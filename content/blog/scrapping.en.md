---
title: "Creating a Dataset from Scratch with Scraping Using Python"
date: 2024-03-13T11:48:52-05:00
draft: false
---

In this post, I will explain how to create a dataset from scratch with scraping using Python. First, I'll introduce the problem we aim to solve.

## Problem Definition

We want to build a neural network for food recognition. Let's split the process into two main steps:

1. **Classes**: First, you need to define the desired classes. If you're unsure, you can start by generating some classes using models like ChatGPT or Gemini.
2. **Scraping**: Once you have the classes, you can create a scraping script to search for images and download them locally in the correct data structure. I find it easier to use the YOLO structure, which consists of the following tree:

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

## Scraping Code

Below is the code that explains how to perform the scraping:

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
    """Compress the image to ensure it is under the specified size (in KB)."""
    quality = 85  # Initial quality setting
    image_format = 'JPEG'
    while True:
        buffer = BytesIO()
        image.save(buffer, format=image_format, quality=quality)
        size_kb = buffer.tell() / 1024
        if size_kb <= max_size_kb or quality <= 10:
            with open(os.path.join(folder_name, image_name), 'wb') as f:
                f.write(buffer.getvalue())
            break
        quality -= 5

def download_image(image_url, folder_name="downloaded_images", image_name="image.jpg"):
    """Download an image from a given URL and save it to the specified folder."""
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
    """Use Selenium to download images from Google Images."""
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
    
    print(f"{keyword}: {len(images)} images found.")
    downloaded_images = 0

    for image in images:
        url = image.get_attribute('src')
        if url != None :
            if 'gif' in url: continue
            download_image(url, folder_name=f"{folder_name}/train/{keyword}", image_name=f"{keyword}_{downloaded_images + 1}.jpg")
            downloaded_images += 1
            if downloaded_images > 50: break

    if len(images) == 0:
        print(f"No images found for {keyword}")
        return keyword
    else:
        return "Good"

def download_images_for_food(food):
    """Download images for a given food item using a headless Chrome browser."""
    chrome_options = Options()
    chrome_options.add_argument("--headless")
    driver = webdriver.Chrome(options=chrome_options)
    try:
        result = download_images_with_selenium(driver, food)
        return result
    finally:
        driver.quit()

def parallel_download_images(foods):
    """Download images in parallel for a list of food items."""
    with ThreadPoolExecutor(max_workers=8) as executor:
        futures = [executor.submit(download_images_for_food, food) for food in foods]
        results = []
        for future in as_completed(futures):
            result = future.result()
            results.append(result)
            print(results)

    # Retry for foods that failed to download images
    failed_downloads = [food for food, result in zip(foods, results) if result != "Good"]
    if failed_downloads:
        print('Retrying failed downloads...')
        return parallel_download_images(failed_downloads)
    return results

def read_txt(file_path):
    """Read a text file and return a list of lines."""
    with open(file_path, 'r') as f:
        return [line.strip() for line in f.readlines()]

# Load the list of food classes from a text file and start downloading images
results = parallel_download_images(read_txt("classes.txt"))
```

## Code Explanation

1. **compress_image**: This function compresses an image to ensure it is under a specified size (in KB) by adjusting the quality parameter. The image is saved once the desired size is reached or the quality is sufficiently reduced.
2. **download_image**: This function downloads an image from a given URL and saves it to a specified folder. It supports both direct URL downloads and base64-encoded images.
3. **download_images_with_selenium**: This function uses Selenium to download images from Google Images based on a keyword. It scrolls through the page to load more images and stops after a few attempts if no more images are loaded. The images are downloaded and saved in a structured folder format.
4. **download_images_for_food**: This function sets up a headless Chrome browser instance to download images for a given food item using the `download_images_with_selenium` function.
5. **parallel_download_images**: This function downloads images for multiple food items in parallel using Python's `ThreadPoolExecutor`. It retries downloading images for food items that failed in the first attempt.
6. **read_txt**: This function reads a text file and returns a list of lines, which represent the food classes to be downloaded.

By following these steps, you can create a dataset for food recognition from scratch using Python and Selenium.

