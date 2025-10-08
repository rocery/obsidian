Algoritma
1. Get String
2. Export To QR Code
3. QR Code to .png
4. .png to .dxf
5. Save

There's no way to convert QR Code directly to .dxf

Algorithm:
1. User input data (csv, xls, xlsx, txt) to a form, the data must 1 column and at least 1 row
2. Convert data to csv
3. Read 1 by 1 and make qr barcode .png formated, name is same as row data
4. Save qr code to a folder
5. Read 1 by 1 qr code, convert it to dxf
6. save dxf in a folder, name is same as row data
7. zip both folder
8. make zip downloadable

i want make it use fastapi