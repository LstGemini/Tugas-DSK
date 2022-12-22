.MODEL SMALL
.CODE

ORG 100h

JMP Mulai

;Variabel
nama    DB 0dh, 0ah, 0dh, 0ah, "Masukan Nama Anda : ", '$'
id      DB 0dh, 0ah, "Masukan nomor antrian Anda : ", '$'
psn1    DB "PROGRAM PENCUCIAN MOBIL", 0dh, 0ah, "----------------------------", '$' 
psn2    DB 0dh, 0dh, 0dh, 0ah, 0dh, 0ah, "Selamat Datang Di Pencucian Latanza ...", '$' 
psn3    DB 0dh, 0dh, 0dh, 0ah, 0dh, 0ah, "Silahkan Pilih Paket anda : ", 0dh, 0ah 
        DB "=====================", 0dh, 0ah
        DB "=   1. Reguler 1    =", 0dh, 0ah
        DB "=   2. Reguler 2    =", 0dh, 0ah
        DB "=   3. Premium      =", 0dh, 0ah
        DB "=   4. Premium +    =", 0dh, 0ah
        DB "=====================", 0dh, 0ah
        DB 0dh, 0ah, "Paket Yang Anda Pilih ? ", '$'

psn4    DB 0dh, 0ah, "Pemilihan Paket Berhasil...", '$'
psn5    DB 0dh, 0dh, 0dh, 0ah, 0dh, 0ah, "========================= PEMILIHAN SELESAI =====================", 0dh, 0ah
        DB "Silahkan letakkan mobil anda dan jangan lupa untuk", 0dh, 0ah, "membawa bukti transaksi yang sudah di cetak", '$'

psn6    DB 0dh, 0dh, 0dh, 0ah, 0dh, 0ah, "Ingin Memilih Paket Lain ? (Y, N)", '$'
psn7    DB 0dh, 0dh, 0dh, 0ah, 0dh, 0ah, "Terimakasih Telah Menggunkan Layanan Ini..", '$'
error   DB 0dh, 0ah, "Masukan Kode Dengan Benar", '$'
msg1    DB 0dh, 0ah, 0dh, 0ah, "====== Reguler 1 ======", 0dh, 0ah, "Paket termasuk cuci biasa", 0dh, 0ah, "Silahkan menunggu di ruang tunggu", 0dh, 0ah, "jika sudah selesai nomor anda akan di panggil" , '$'
msg2    DB 0dh, 0ah, 0dh, 0ah, "====== Reguler 2 ======", 0dh, 0ah, "Paket termasuk cuci + parfum", 0dh, 0ah, "Silahkan menunggu di ruang tunggu", 0dh, 0ah, "jika sudah selesai nomor anda akan di panggil" , '$'
msg3    DB 0dh, 0ah, 0dh, 0ah, "====== Premium ======", 0dh, 0ah, "Paket termasuk cuci + parfum + wax", 0dh, 0ah, "Silahkan menunggu di ruang tunggu", 0dh, 0ah, "jika sudah selesai nomor anda akan di panggil" , '$'
msg4    DB 0dh, 0ah, 0dh, 0ah, "====== Premium + ======", 0dh, 0ah, "Paket termasuk cuci + parfum + wax + detailing", 0dh, 0ah, "Silahkan menunggu di ruang tunggu", 0dh, 0ah, "jika sudah selesai nomor anda akan di panggil" , '$'
msg5    DB 0dh, 0ah, 0dh, 0ah, "Ketik 'E' Untuk Mencetak Bukti dan Keluar dari program.... ", '$'

tampung_nama DB 30, ?, 30 dup(?)
tampung_id DB 30, ?, 30 dup(?)
        
        
Mulai:
    MOV ah, 09
    LEA dx, psn1
    INT 21h
    
    MOV ah, 09
    LEA dx, nama
    INT 21h
    
    MOV ah, 0ah
    LEA dx, tampung_nama
    INT 21h
    PUSH dx
    
    MOV ah, 09
    LEA dx, id
    INT 21h
    
    MOV ah, 0ah
    LEA dx, tampung_id
    INT 21h
    PUSH dx
    
    MOV ah, 09
    LEA dx, psn2
    INT 21h
    
Mulai2:
    MOV ah, 09
    LEA dx, psn3
    INT 21h
    
Proses:
    MOV ah, 01
    INT 21h
    
    CMP al, '1'
    JE barang_1
    
    CMP al, '2'
    JE barang_2
    
    CMP al, '3'
    JE barang_3
    
    CMP al, '4'
    JE barang_4
    
    JNE psn_error
    
Proses2:
    MOV ah, 09
    LEA dx, psn6
    INT 21h
    MOV ah, 01
    INT 21h
    
    CMP al, 'Y'
    JE pilih_lagi
    
    CMP al, 'y'
    JE pilih_lagi
    
    CMP al, 'N'
    JE pilih_selesai
    
    CMP al, 'n'
    JE pilih_selesai
    
    JNE psn_error2

barang_1:
     MOV ah, 09
     LEA dx, psn4
     INT 21h
     
     MOV ah, 09
     LEA dx, msg1
     INT 21h   
     
     JMP Proses2
     
barang_2:
     MOV ah, 09
     LEA dx, psn4
     INT 21h
     
     MOV ah, 09
     LEA dx, msg2
     INT 21h   
     
     JMP Proses2

barang_3:
     MOV ah, 09
     LEA dx, psn4
     INT 21h
     
     MOV ah, 09
     LEA dx, msg3
     INT 21h   
     
     JMP Proses2 
     
barang_4:
     MOV ah, 09
     LEA dx, psn4
     INT 21h
     
     MOV ah, 09
     LEA dx, msg4
     INT 21h   
     
     JMP Proses2

pilih_lagi:
    JMP Mulai2

pilih_selesai:
    MOV ah, 09
    LEA dx, psn5
    INT 21h
    JMP Konfirmasi

psn_error:
    MOV ah, 09
    LEA dx, error
    INT 21h
    
    JMP Mulai2

psn_error2:
    MOV ah, 09
    LEA dx, error
    INT 21h
    
    JMP Proses2

Konfirmasi:
    MOV ah, 09
    LEA dx, msg5
    INT 21h
    MOV ah, 01
    INT 21h
    
    CMP al, 'E'
    JE Exit
    
    CMP al, 'e'
    JE Exit
    
    JNE psn_error
    
 

JMP Exit

Exit:
    MOV ah, 09
    LEA dx, psn7
    INT 21h 
    
    INT 20h
     
RET
