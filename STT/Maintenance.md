https://kelasrobot.com/tutorial-gm66-uart-qrcode-barcode-for-arduino/
itsttbekasi@gmail.com

tgl_user_approve = Tanggal selesai
mail = tangl kirim email
tgl_selesai = tanggal ok

SELECT idm, tanggal, id_div, nama_user, tgl_user_approve, nama_user_approve, mail, status_mtc, tgl_selesai FROM sistemit.mtc_checklist
WHERE 1 = 1
AND pic = "sastra"
-- AND (idm = 7 OR idm = 6)
AND idm = 7
AND id_div = "PRD"
ORDER BY nama_user