import random

# Membuat grid 4x4
grid = [
   [0, 0, 0, 0],  # r0
   [0, 0, 0, 0],  # r1
   [0, 0, 0, 0],  # r2
   [0, 0, 0, 0]   # r3
]

# Inisialisasi skor
score = 0

# Fungsi untuk menampilkan grid dan skor
def display_grid():
    for i in range(4):
        for j in range(4):
            print(f"{grid[i][j]:4}", end=' ')
        print()
    print(f"Skor: {score}\n")

# Fungsi untuk menambahkan angka 2 di posisi kosong acak
def add_random_2():
    row = random.randint(0, 3)
    column = random.randint(0, 3)
    while grid[row][column] != 0:
        row = random.randint(0, 3)
        column = random.randint(0, 3)
    grid[row][column] = 2

# Fungsi untuk menggabungkan angka dan menambah skor
def merge(lst):
    global score
    # Buang angka 0 dari list terlebih dahulu
    lst = [x for x in lst if x != 0]
    merged = []
    skip = False
    for i in range(len(lst)):
        if skip:
            skip = False
            continue
        if i + 1 < len(lst) and lst[i] == lst[i + 1]: 
            merged.append(lst[i] * 2)
            score += lst[i] * 2  # Tambah skor sesuai dengan penggabungan
            skip = True
        else:
            merged.append(lst[i])
    # Tambah angka 0 di akhir untuk menyesuaikan panjang list
    merged.extend([0] * (4 - len(merged)))
    return merged

# Fungsi untuk memindahkan dan menggabungkan angka sesuai dengan arah
def move_and_merge(direction):
    global grid
    moved = False
    if direction == 'w':  # Gerakan ke atas
        for i in range(4):  # Iterasi kolom
            temp = [grid[j][i] for j in range(4)]
            temp = merge(temp)
            for j in range(4):
                if grid[j][i] != temp[j]:
                    moved = True
                grid[j][i] = temp[j]
                
    elif direction == 'a':  # Gerakan ke kiri
        for i in range(4):  # Iterasi baris
            temp = [grid[i][j] for j in range(4)]
            temp = merge(temp)
            for j in range(4):
                if grid[i][j] != temp[j]:
                    moved = True
                grid[i][j] = temp[j]
                
    elif direction == 's':  # Gerakan ke bawah
        for i in range(4):  # Iterasi kolom
            temp = [grid[j][i] for j in range(3, -1, -1)]
            temp = merge(temp)
            for j in range(4):
                if grid[3-j][i] != temp[j]:
                    moved = True
                grid[3-j][i] = temp[j]

    elif direction == 'd':  # Gerakan ke kanan
        for i in range(4):  # Iterasi baris
            temp = [grid[i][j] for j in range(3, -1, -1)]
            temp = merge(temp)
            for j in range(4):
                if grid[i][3-j] != temp[j]:
                    moved = True
                grid[i][3-j] = temp[j]
                
    return moved

# Fungsi untuk memeriksa apakah ada ruang kosong atau pergerakan yang mungkin
def can_move_or_merge():
    # Memeriksa jika ada sel kosong
    for i in range(4):
        for j in range(4):
            if grid[i][j] == 0:
                return True
            # Memeriksa apakah ada angka yang bisa digabungkan
            if i < 3 and grid[i][j] == grid[i+1][j]:  # Cek ke bawah
                return True
            if j < 3 and grid[i][j] == grid[i][j+1]:  # Cek ke kanan
                return True
    return False

# kondisi memang 
def check_win():
    # Memeriksa apakah ada angka 2048 dalam grid
    for i in range(4):
        for j in range(4):
            if grid[i][j] == 2048:
                return True
    return False

print(" selamat datang di game 2048! ")

# Posisi angka 2 pertama
add_random_2()

# Posisi angka 2 kedua
add_random_2()

# Implementasi kontrol dan skor
while True:

    display_grid()
    arah = input("Perintah (w/a/s/d untuk gerak, q untuk keluar): ").lower()

    if arah == 'q':  # Keluar dari permainan
        print("Game Over!")
        break

    # Lakukan pergerakan dan penggabungan sekali
    moved = move_and_merge(arah)

    # Jika ada pergerakan, tambahkan angka 2 di grid
    if moved:
        add_random_2()

    # Cek apakah permainan berakhir (grid penuh dan tidak ada pergerakan)
    if not can_move_or_merge():
        print("Permainan berakhir! Tidak ada pergerakan atau penggabungan yang mungkin.")
        break

    # Cek apakah pemain sudah menang
    if check_win():
        print("Selamat! Anda telah memenangkan permainan!")
        break
