# Fastapi receive a xlsx file and read it

How to accept a xlsx file and read it using Fastapi, the following is the implementation code.
```
@application.post("/uploadFile/")
async def create_upload_file(file: UploadFile):
    if file.filename.endswith('.xlsx'):
        # Read it, 'f' type is bytes
        f = await file.read()
        xlsx = io.BytesIO(f)
        wb = openpyxl.load_workbook(xlsx)
        ws = wb['Sheet1']

        for cells in ws.iter_rows():
            print([cell.value for cell in cells])
        return True

    else:
        raise HTTPException(status_code=status.HTTP_405_METHOD_NOT_ALLOWED)
``` 
