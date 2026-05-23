# bitmap-editor

A Windows hex editor for BMP files (C# WinForms). Opens a `.bmp` file, displays its raw bytes as hex, and parses the BMP structure field by field — header, info header, color table, and pixel data — into separate editable fields. Modified hex can be saved back as a valid binary file.

---

## How it works

### Opening a file
- Reads the entire `.bmp` file as raw bytes
- Displays all bytes as hex in a main text box (space-separated, e.g. `42 4d 36 ...`)
- Parses the BMP binary structure into individual fields:

**BITMAPFILEHEADER** (14 bytes):
| Field | Size | Description |
|---|---|---|
| bfType | 2 bytes | File signature (`42 4d` = "BM") |
| bfSize | 4 bytes | Total file size |
| bfReserved1 | 2 bytes | Reserved |
| bfReserved2 | 2 bytes | Reserved |
| bfOffBits | 4 bytes | Offset to pixel data |

**BITMAPINFOHEADER** (40 bytes):
| Field | Size | Description |
|---|---|---|
| biSize | 4 bytes | Header size |
| biWidth / biHeight | 4 bytes each | Image dimensions |
| biPlanes | 2 bytes | Color planes |
| biBitCount | 2 bytes | Bits per pixel |
| biCompression | 4 bytes | Compression type |
| biSizeImage | 4 bytes | Image data size |
| biXPelsPerMeter / biYPelsPerMeter | 4 bytes each | DPI |
| biClrUsed / biClrImportant | 4 bytes each | Color table info |

- Pixel data displayed separately after the color table (16-color palette, 4 bytes per entry)

### Editing and saving
- Edit any hex value directly in the main text box
- Save parses the space-separated hex back to bytes and writes the binary file

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | C# |
| Framework | .NET Core 3.1, WinForms |
| Platform | Windows |

---

## Running the project

Open in Visual Studio, build and run. Or run the compiled `.exe` from `bin/Debug/netcoreapp3.1/`.
