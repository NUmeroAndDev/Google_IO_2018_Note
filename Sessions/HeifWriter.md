# HeifWriter

API 28+

### Writing to a HEIF file

```
val builder = HeifWriter.Builder("path/to/file", 100, 100, HeifWriter.INPUT_MODE_BITMAP)
builder.setQuality(80)
val heifWriter = builder.build().apply {
  start()
  addBitmap(bitmap1)
  addBitmap(bitmap2)
  stop(1000)  // 1000はタイムアウト
  close()
}
```


