# Pandoc
## Installation On MacOS
1. Open terminal and run the following command:
  ```
  brew install pandoc
  ```
2. Install pdf engine by running the command:
  ```
  brew install basictex // For lightweight installation
  // Or
  brew install --cask mactex // For full installation
  ```
3. Verify the installation by checking the version:
  ```
  pandoc --version
  ```

## Basic Usage
### Convert Markdown to PDF
- If mactex is installed, run the following command:
```
pandoc <input_file_name>.md -o <output_file_name>.pdf
```
If not, a pdf engine needs to be installed separately and specified using `--pdf-engine` flag:
- For embedding images, use `--resource-path` flag to specify the directory containing the images.
```
// In the path where the markdown file is located, exists an "images" folder containing images referred
to by the markdown file.
pandoc <input_file_name>.md -o <output_file_name>.pdf --resource-path=.:/images
```