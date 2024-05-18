---
title: "Creación de un Conjunto de Datos desde Cero con Scraping Usando Python"
date: 2024-03-13T11:48:52-05:00
draft: false
---
 
En esta publicación, explicaré cómo crear un conjunto de datos desde cero con scraping usando Python. Primero, presentaré el problema que queremos resolver.

## Definición del Problema

Queremos construir una red neuronal para el reconocimiento de alimentos. Vamos a dividir el proceso en dos pasos principales:

1. **Clases**: Primero, necesitas definir las clases deseadas. Si no estás seguro, puedes comenzar generando algunas clases usando modelos como ChatGPT o Gemini.
2. **Scraping**: Una vez que tengas las clases, puedes crear un script de scraping para buscar imágenes y descargarlas localmente en la estructura de datos correcta. Encuentro más fácil usar la estructura de YOLO, que consiste en el siguiente árbol:

   ```
   ├───Dataset
   │   ├───Train
   │   │   ├───pizza
   │   │   │   ├───1.jpg
   │   │   │   ├───2.jpg
   │   │   │   ├───3.jpg
   │   │   ├───rice
   │   │   │   ├───1.jpg
   │   │   │   ├───2.jpg
   │   │   │   ├───3.jpg
   │   │   ├───hamburguer
   │   │   │   ├───1.jpg
   │   │   │   ├───2.jpg
   │   │   │   ├───3.jpg
   ```

## Código de Scraping

A continuación se muestra el código que explica cómo realizar el scraping:

```python
import os
import time
import requests
import base64
from PIL import Image
from io import BytesIO
from concurrent.futures import ThreadPoolExecutor, as_completed
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By

def compress_image(image, folder_name, image_name, max_size_kb=5):
    """Comprime la imagen para asegurarse de que esté por debajo del tamaño especificado (en KB)."""
    quality = 85  # Configuración de calidad inicial
    image_format = 'JPEG'
    while True:
        buffer = BytesIO()
        image.save(buffer, format=image_format, quality=quality)
        size_kb = buffer.tell() / 1024
        if size_kb <= max_size_kb o quality <= 10:
            with open(os.path.join(folder_name, image_name), 'wb') as f:
                f.write(buffer.getvalue())
            break
        quality -= 5

def download_image(image_url, folder_name="downloaded_images", image_name="image.jpg"):
    """Descarga una imagen de una URL dada y la guarda en la carpeta especificada."""
    os.makedirs(folder_name, exist_ok=True)
    if "https://" in image_url:
        response = requests.get(image_url)
        response.raise_for_status()
        image = Image.open(BytesIO(response.content))
    elif any(ext in image_url for ext in ['jpeg', 'jpg', 'png']):
        base64_str = image_url.split(",")[1]
        image_data = base64.b64decode(base64_str)
        image = Image.open(BytesIO(image_data))
    
    image = image.convert('RGB')
    compress_image(image, folder_name, image_name)

def download_images_with_selenium(driver, keyword, folder_name="Recipes10T"):
    """Usa Selenium para descargar imágenes de Google Imágenes."""
    driver.get(f'https://www.google.com/search?hl=en&q={keyword + " food"}&tbm=isch')
    
    images = []
    previous_len_images = 0
    scroll_attempts = 0

    while scroll_attempts < 5:
        images = [img for img in driver.find_elements(By.CSS_SELECTOR, '.H8Rx8c img.YQ4gaf') if int(img.get_attribute('height')) > 100]
        current_len_images = len(images)

        if current_len_images > previous_len_images:
            driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
            previous_len_images = current_len_images
            time.sleep(5)
            scroll_attempts += 1
        else:
            break
    
    print(f"{keyword}: {len(images)} imágenes encontradas.")
    downloaded_images = 0

    for image in images:
        url = image.get_attribute('src')
        if url != None :
            if 'gif' in url: continue
            download_image(url, folder_name=f"{folder_name}/train/{keyword}", image_name=f"{keyword}_{downloaded_images + 1}.jpg")
            downloaded_images += 1
            if downloaded_images > 50: break

    if len(images) == 0:
        print(f"No se encontraron imágenes para {keyword}")
        return keyword
    else:
        return "Good"

def download_images_for_food(food):
    """Descarga imágenes para un alimento dado usando un navegador Chrome sin cabeza."""
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    driver = webdriver.Chrome(options=chrome_options)
    try:
        result = download_images_with_selenium(driver, food)
        return result
    finally:
        driver.quit()

def parallel_download_images(foods):
    """Descarga imágenes en paralelo para una lista de alimentos."""
    with ThreadPoolExecutor(max_workers=8) as executor:
        futures = [executor.submit(download_images_for_food, food) for food in foods]
        results = []
        for future in as_completed(futures):
            result = future.result()
            results.append(result)
            print(results)

    # Reintentar para los alimentos que no se pudieron descargar imágenes
    failed_downloads = [food for food, result in zip(foods, results) if result != "Good"]
    if failed_downloads:
        print('Reintentando descargas fallidas...')
        return parallel_download_images(failed_downloads)
    return results

def read_txt(file_path):
    """Lee un archivo de texto y devuelve una lista de líneas."""
    with open(file_path, 'r') as f:
        return [line.strip() for line in f.readlines()]

# Cargar la lista de clases de alimentos desde un archivo de texto y comenzar a descargar imágenes
results = parallel_download_images(read_txt("classes.txt"))
```

## Explicación del Código

1. **compress_image**: Esta función comprime una imagen para asegurarse de que esté por debajo de un tamaño especificado (en KB) ajustando el parámetro de calidad. La imagen se guarda una vez que se alcanza el tamaño deseado o se reduce suficientemente la calidad.
2. **download_image**: Esta función descarga una imagen de una URL dada y la guarda en una carpeta especificada. Soporta tanto descargas directas desde URL como imágenes codificadas en base64.
3. **download_images_with_selenium**: Esta función utiliza Selenium para descargar imágenes de Google Imágenes basándose en una palabra clave. Se desplaza por la página para cargar más imágenes y se detiene después de unos intentos si no se cargan más imágenes. Las imágenes se descargan y guardan en una estructura de carpetas organizada.
4. **download_images_for_food**: Esta función configura una instancia del navegador Chrome sin cabeza para descargar imágenes de un alimento dado usando la función `download_images_with_selenium`.
5. **parallel_download_images**: Esta función descarga imágenes para múltiples alimentos en paralelo usando `ThreadPoolExecutor` de Python. Vuelve a intentar descargar imágenes para los alimentos que fallaron en el primer intento.
6. **read_txt**: Esta función lee un archivo de texto y devuelve una lista de líneas, que representan las clases de alimentos a descargar.

Siguiendo estos pasos, puedes crear un conjunto de datos para el reconocimiento de alimentos desde cero usando Python y Selenium.

