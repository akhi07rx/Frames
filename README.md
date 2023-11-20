# Frame Extractor

This Python script allows you to extract frames from a video file and save them into a zip file. The frames are saved as PNG images.

## Dependencies

The script requires the following Python libraries:

- OpenCV (`cv2`)
- `os`
- `zipfile`

You can install these dependencies using pip:

```bash
pip install opencv-python
```

## Usage

To use the script, you need to provide the path to the video file and the output folder where the frames will be saved. The script will create a zip file named `frames.zip` in the output folder.

Here is the main function of the script:

```python
def extract_frames(video_path, output_folder):
    video = cv2.VideoCapture(video_path)
    frame_count = 0

    with zipfile.ZipFile(os.path.join(output_folder, "frames.zip"), 'w') as zipf:
        while True:
            ret, frame = video.read()
            if not ret:
                break

            output_path = os.path.join(output_folder, f"frame_{frame_count}.png")
            cv2.imwrite(output_path, frame)
            zipf.write(output_path)
            os.remove(output_path)

            frame_count += 1
    video.release()
```

You can run the script in the terminal as follows:

```bash
python script.py
```

When prompted, enter the path to the video file and the output folder:

```bash
Enter the path to the video file: /path/to/video.mp4
Enter the path to the output folder: /path/to/output/folder
```

The script will then extract the frames from the video and save them into a zip file in the output folder.
