import os
from PIL import Image

def create_tiff_layout(images_folder, output_filename, images_per_row, padding, background_color, side_border, top_bottom_border, resolution):
    images = [Image.open(os.path.join(images_folder, img)) for img in os.listdir(images_folder) if img.endswith('.png')]
    images.reverse()  # Меняем порядок изображений на обратный
    
    max_width = max(i.width for i in images)
    max_height = max(i.height for i in images)
    
    total_width = max_width * images_per_row + padding * (images_per_row - 1) + side_border * 2
    rows = (len(images) + images_per_row - 1) // images_per_row
    total_height = max_height * rows + padding * (rows - 1) + top_bottom_border * 2
    
    result_image = Image.new('RGB', (total_width, total_height), color=background_color)
    
    x_offset = side_border
    y_offset = top_bottom_border
    for i, img in enumerate(images):
        if i % images_per_row == 0 and i != 0:
            y_offset += max_height + padding
            x_offset = side_border
        x_centered = x_offset + (max_width - img.width) // 2
        y_centered = y_offset + (max_height - img.height) // 2
        result_image.paste(img, (x_centered, y_centered))
        x_offset += max_width + padding
    
    result_image = result_image.resize((1000, 600), Image.Resampling.LANCZOS)
    result_image.info['dpi'] = resolution
    
    result_image.save(output_filename, 'TIFF')

folder_path = r'путь к папке'
create_tiff_layout(folder_path, 'Result.tif', 4, 140, 'white', 380, 500, (72, 72))  
