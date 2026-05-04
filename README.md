
Commit README vào repo public.

---

# 8. Nên thêm release body tự động

Hiện tại release page có thể hơi trống. Bạn có thể tạo file release note tự động trong workflow.

Trong `release.yml`, thêm step này **trước** step `Create public GitHub Release`:

```yaml
- name: Create release notes
  shell: pwsh
  run: |
    $tag = "${{ github.ref_name }}"
    $downloadFile = $env:ZIP_NAME

    @"
    # ValorantTweaks.App $tag

    ## Download

    Download:

    - $downloadFile

    ## How to use

    1. Download the ZIP file.
    2. Extract the ZIP file to a normal folder.
    3. Open the extracted folder.
    4. Run:

       ````text
       ValorantTweaks.App.exe
       ````

    5. Do not run the app directly inside the ZIP file.

    ## Requirements

    - Windows 10 version 1809 or newer
    - Windows x64

    ## Notes

    If Windows SmartScreen appears, click:

    ````text
    More info → Run anyway
    ````

    This warning may appear because the app is not code-signed yet.
    "@ | Set-Content -Path RELEASE_NOTES.md -Encoding UTF8
