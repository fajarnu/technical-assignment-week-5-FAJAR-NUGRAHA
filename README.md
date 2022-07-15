import time #mengimport modul time
import board #digunakan untuk menentukan dengan pin GPIO mana kita menghubungkan sensor DHT11.
import adafruit_dht #library sensor DHT
import psutil #library untuk mengambil informasi tentang proses yang sedang berjalan


for proc in psutil.process_iter(): 
    if proc.name() == 'libgpiod_pulsein' or proc.name() == 'libgpiod_pulsei':
        proc.kill()
sensor = Adafruit_DHT.DHT11 
DHT_PIN = 4 #mendefinisikan pin data sensor. Ubah nomor pin jika ingin menggunakan pin lain.
while True: #pengkondisian 
    try:
        humidity, temperature = Adafruit_DHT. read(sensor, DHT_PIN) #membaca nilai kelembaban dan suhu
        print("Temperature: {}*C Humidity: {}".format(temperature, humidity)) #mencetak hasilnya di layar. Mempertimbangkan akurasi sensor yang terbatas, hasilnya diformat tanpa desimal. 
    except RuntimeError as error: #dijalankan ketika runtime error
        print(error.args[0]) 
        time.sleep(1.0) #program akan diulang setiap 1 detik
        continue
    except Exception as error: #dijalankan ketika pengecualian error 
        sensor.exit()
        raise error
    time.sleep(1.0) #program akan diulang setiap 1 detik
