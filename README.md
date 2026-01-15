# Face Recognition System

A Python-based face recognition system that can train on known faces and identify them in unknown images.

## Features

- **Train**: Build encodings from training images
- **Validate**: Test the model against validation images
- **Test**: Identify faces in unknown images
- Draws bounding boxes around detected faces with name labels
- Saves annotated output images

## Prerequisites

- **Python**: 3.10.x (tested with Python 3.10.19)
- **CMake**: Required for building dlib
- **pip**: Python package installer

## Project Structure

```
face_recognizer/
├── detector.py           # Main face recognition script
├── requirements.txt      # Python dependencies
├── training/            # Training images organized by name
│   ├── Ahmed/          # Folder with Ahmed's images
│   └── Mujtaba/        # Folder with Mujtaba's images
├── validation/         # Validation images (optional)
├── output/             # Generated encodings and result images
│   ├── encodings.pkl   # Trained face encodings
│   └── recognized_*.jpeg  # Annotated output images
└── .venv/              # Virtual environment (created during setup)
```

## Installation

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd face_recognizer
```

### 2. Create a Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install --upgrade pip
pip install cmake
pip install -r requirements.txt
```

**Note**: Installing `dlib` may take several minutes as it compiles from source.

## Usage

### Training the Model

1. **Prepare Training Data**: Add images to the `training/` directory, organized by person name:
   ```
   training/
   ├── PersonName1/
   │   ├── image1.jpg
   │   └── image2.jpg
   └── PersonName2/
       ├── image1.jpg
       └── image2.jpg
   ```

2. **Run Training**:
   ```bash
   python detector.py --train
   ```
   This creates `output/encodings.pkl` with the trained face encodings.

### Testing with Unknown Images

Run face recognition on an unknown image:

```bash
python detector.py --test -f path/to/unknown_image.jpg
```

**Output**: 
- Annotated image saved to `output/recognized_<filename>.jpg`
- Displays the image with bounding boxes and name labels

**Example**:
```bash
python detector.py --test -f Unknown.jpeg
```

### Validating the Model

Test the model against validation images:

```bash
python detector.py --validate
```

Place validation images in the `validation/` directory.

## Command-Line Options

| Option | Description |
|--------|-------------|
| `--train` | Train the model on images in the `training/` folder |
| `--validate` | Validate the model using images in the `validation/` folder |
| `--test` | Test the model with an unknown image |
| `-f <path>` | Path to the image file for testing |
| `-m <model>` | Model to use: `hog` (CPU, default) or `cnn` (GPU) |

### Examples

```bash
# Train with HOG model (CPU)
python detector.py --train -m hog

# Train with CNN model (GPU - faster but requires CUDA)
python detector.py --train -m cnn

# Test with CNN model
python detector.py --test -f Unknown.jpeg -m cnn
```

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| dlib | 19.24.0 | Face detection and recognition library |
| face-recognition | 1.3.0 | High-level face recognition wrapper |
| numpy | 1.24.2 | Numerical computing |
| Pillow | 9.4.0 | Image processing |

## Troubleshooting

### dlib Installation Fails

If `dlib` fails to install:

1. **Install CMake first**:
   ```bash
   pip install cmake
   ```

2. **Install system dependencies** (Linux):
   ```bash
   sudo apt-get update
   sudo apt-get install build-essential cmake
   ```

3. **Try installing without version pinning**:
   ```bash
   pip install dlib
   ```

### No Faces Detected

- Ensure images are clear and faces are visible
- Try using the CNN model: `-m cnn` (requires more resources)
- Check image quality and lighting

### Permission Errors

Make sure you have write permissions for the `output/` directory:
```bash
chmod -R 755 output/
```

## Output

When testing with an unknown image:
- **Console**: Prints the save location
- **File**: Annotated image saved to `output/recognized_<filename>`
- **Display**: Opens the annotated image (if display is available)

## Performance

- **HOG model**: Faster, works on CPU, good for most cases
- **CNN model**: More accurate, requires GPU (CUDA), slower on CPU

## License

Free to use and modify.

## Author

Created for face identification purposes.
# face_Recogziner
