# QuestionOCR Mobile

A mobile-first, browser-based tool for extracting Chinese question text from multiple photos. It supports batch cropping at the same relative position, local OCR, structured question formatting, text editing, and bulk copy/export.

## Features

- Select multiple images from a phone or computer.
- Draw, move, and resize a crop rectangle with touch gestures.
- Apply one normalized crop region to every source image.
- Preview crops before running recognition.
- Read Simplified Chinese text with PP-OCRv5 through PaddleOCR.js.
- Format multiple-choice (A-D/A-E) and true/false questions without guessing answers.
- Review the original recognized lines, correct text manually, and select which results to export.
- Copy selected text or save a UTF-8 TXT file.
- Convert commonly recognized Traditional Chinese characters to Simplified Chinese.
- Process images on the device rather than uploading them to an application backend.

## Use on a phone

1. Open the deployed HTTPS website in Safari, Chrome, or another modern browser.
2. Select the photos to process.
3. Draw a crop rectangle on the reference photo. The same relative crop coordinates are applied to the remaining photos.
4. Use **Preview all crops** to check that the question and options are inside the rectangle.
5. Select a question format and recognition settings.
6. Tap **Start batch OCR** and wait for each image to finish.
7. Edit the recognized text, select the desired results, and copy or export them.

The user interface is in Simplified Chinese.

## Deploy to GitHub Pages

This is a static site with no build step. The repository root contains `index.html`.

1. Create a GitHub repository and upload the files from this project into its root directory.
2. In **Settings > Pages > Build and deployment**, select **Deploy from a branch**.
3. Choose `main` and `/(root)`, then save.
4. Open the Pages address shown in the GitHub repository settings.

For a repository named `QuestionOCRMobile`, a typical project Pages URL is `https://USERNAME.github.io/QuestionOCRMobile/`. A user site repository named `USERNAME.github.io` publishes at its corresponding root address instead.

## Technical notes

- The OCR engine uses the `@paddleocr/paddleocr-js` browser SDK and the PP-OCRv5 Chinese model.
- The PaddleOCR.js package is pinned to `0.4.2`, and ONNX Runtime WASM resources are pinned to `1.24.3`.
- On first use, the browser downloads JavaScript, WASM, and OCR models from third-party CDNs/model hosts. An internet connection and access to those endpoints are required. Local inference is not the same as a fully offline or self-contained installation.
- Images are processed locally in browser memory and are not intentionally sent to this website's server. Browser extensions, third-party libraries, and the hosting environment are outside the application's control.
- The app decodes one full-resolution photo at a time for cropping, releases temporary bitmaps and canvases, and reduces OCR input dimensions on iOS. These changes reduce memory pressure but do not guarantee compatibility with every iPhone or Android device.
- Camera blur, screen moire, low-resolution text, and unusual fonts can reduce OCR accuracy. Verify critical content manually.
- The crop region uses normalized coordinates and works best when all photos have similar framing; automatic screen/perspective correction is **not** implemented.
- The project is a web app, not an Android APK or iOS native app.

## Troubleshooting

- **Failed to fetch**: verify HTTPS access and availability of the third-party model/CDN endpoints. Opening `index.html` directly through `file://` is not supported for OCR.
- **The page reloads while loading models**: the browser may be exceeding the device's memory budget. Close other tabs, select fewer images, and try the **Load model only** diagnostic action.
- **Recognition contains incorrect characters**: crop more tightly around the text, use the original-color preprocessing mode, and review the raw OCR lines.
- **Copy does not work**: use an HTTPS address and try the browser's manual selection/copy feature.

## Credits

The OCR pipeline uses [PaddleOCR.js](https://github.com/PaddlePaddle/PaddleOCR) and ONNX Runtime Web. Traditional-to-Simplified character conversion includes data derived from [OpenCC](https://github.com/BYVoid/OpenCC). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## License

MIT for the original application code. Third-party software and data retain their respective licenses; see [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
