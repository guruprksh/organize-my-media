# Privacy

- **Your files** are read locally by the browser. They are not uploaded anywhere.
- **Without Claude vision**, nothing leaves your device.
- **With Claude vision**, 512 px JPEG previews of photos (and one frame per video), plus file names and last-modified dates, are sent to the Anthropic API in batches. See Anthropic's privacy policy for how API data is handled.
- **Your API key** is kept in memory for the open tab only. It is not written to localStorage, cookies or any file.
- **Fonts** are loaded from Google Fonts. Remove the `<link>` in `index.html` to avoid that request.
- There is no analytics, tracking or backend.
