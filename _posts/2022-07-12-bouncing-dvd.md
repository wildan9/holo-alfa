---
title: Membuat "Bouncing DVD" menggunakan C++
---

Pada kesempatan kali ini, saya akan memperlihatkan sebuah karya yang saya buat dan menjelaskan bagaimana saya membuatnya. <!--more-->Baiklah, tanpa berlama-lama lagi, saya akan memperlihatkan hasil karya saya dan akan dilanjutkan dengan penjelasan bagaimana saya membuatnya.

## Ini dia hasilnya

.......
![DVD]({{ site.url }}/img/posts/2022.07.12-21.52_1.gif)

## Penjelasan bagaimana membuat "Bouncing DVD" menggunakan C++

Sebelumnya saya asumsikan bahwa teman-teman sudah menginstall dan mensetup compiler C/C++ dan raylib. Dan tentunya kita sudah dapat meng-include header file `raylib.h` seperti ini `#include "raylib.h"`, karena nantinya hanya itu header file yang akan kita tulis disni.

* Untuk menggambar sebuah text bertuliskan "DVD", kita dapat menggunakan fungsi:
{% highlight cpp %}
 void DrawText(const char *text, int posX, int posY, int fontSize, Color color);
{% endhighlight %} 

* Pada fungsi diatas dapat kita lihat, parameter pertama adalah text yang akan digambar dan ada 2 parameter untuk menentukan posisinya serta 1 dibagian ujung kanan untuk menentukan warnanya. Kita buat 2 buah Vector2 yang satu berisi posisi "DVD" yang satunya lagi kecepatan perpindahan posisi "DVD". Disini kita menggunakan fungsi `GetScreenWidth()` dan `GetScreenHeight()` untuk mendapatkan lebar dan tinggi layar yang digunakan untuk menentukan posisi awal "DVD".
{% highlight cpp %}
#include "raylib.h"

int main()
{
    Vector2 textPos = { GetScreenWidth() / 2.0f, GetScreenHeight() / 2.0f }; // posisi text
    Vector2 speed = { 4.5f, 2.0f }; // kecepatan perpindahan "DVD"

    return 0;
}
{% endhighlight %}

* Kemudian dilanjutkan dengan membuat array dari sekumpulan warna yang nantinya warna-warna inilah yang menjadi warna "DVD" yang berganti-ganti, tidak lupa juga kita membuat sebuah warna yang menjadi warna awal "DVD".
{% highlight cpp %}
#include "raylib.h"

int main()
{
    .......
    Color arrColor[] = { RED, BROWN, YELLOW, GREEN, PINK, BLUE, PURPLE, GOLD }; // kumpulan warna
    Color textColor = BLUE; // warna

    return 0;
}
{% endhighlight %}

* Set target FPS menggunakan fungsi `SetTargetFPS(int fps)`, sedangkan untuk menciptakan sebuah window, kita menggunakan fungsi `InitWindow(` `int width, int height, const char *title)` dan untuk kedua fungsi tersebut langsung saja kita tuliskan argumentnya.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    InitWindow(800, 450, "Bouncing DVD"); // menginisialisasi window
    SetTargetFPS(60); // menset target fps

    .......

    return 0;
}
{% endhighlight %}

* Membuat while loop dan menggunakan fungsi `WindowShouldClose()` untuk mengecek apakah tombol KEY_ESCAPE atau Close icon ditekan, jika benar, maka loop di akhiri.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    ........
    ........
    while (!WindowShouldClose())
    {
        ........
    }

    return 0;
}
{% endhighlight %}

* Memanggil fungsi `BeginDrawing(void)` dan `EndDrawing(void)` untuk mulai menggambar dan menyudahi.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    .......
    .......
    while (!WindowShouldClose())
    {
        .......
        BeginDrawing(); // mulai menggambar
        .......
        .......
        EndDrawing(); // menyudahi menggambar
    }

    return 0;
}
{% endhighlight %}

* Menggunakan fungsi `ClearBackground(Color color)` untuk menset warna background.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    ........
    ........
    while (!WindowShouldClose())
    {
        ........
        ClearBackground(BLACK); // kita set dengan warna hitam
        ........
    }

    return 0;
}
{% endhighlight %}

* Menggunakan fungsi `GetRandomValue(int min, int max)` untuk mengambil warna secara random, dan 2 buah `if` untuk melalukan perpindahan posisi "DVD" disertai dengan pengambilan warna secara random. Untuk mendapatkan lebar dan tinggi layar yang digunakan untuk menentukan batas pergerakan "DVD", kita menggunakan fungsi `GetScreenWidth()` dan `GetScreenHeight()`.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    ........
    ........
    while (!WindowShouldClose())
    {
        ........
        textPos.x += speed.x;
        textPos.y += speed.y;

        if (textPos.x >= (GetScreenWidth() - 150.0f) || textPos.x <= 0)
        {
            speed.x *= -1.0f;
            textColor = arrColor[GetRandomValue(0, 8)];
        }
        if (textPos.y >= (GetScreenHeight() - 70.0f) || textPos.y <= 0)
        {
            speed.y *= -1.0f;
            textColor = arrColor[GetRandomValue(0, 8)];
        }
        ........
    }

    return 0;
}
{% endhighlight %}

* Dan akhirnya kita dapat menggunakan fungsi `DrawText(const char *text, int posX, int posY, int fontSize, Color color)` untuk menggambar tulisan "DVD".
{% highlight cpp %}
#include "raylib.h"

int main()
{
    ........
    ........
    while (!WindowShouldClose())
    {
        ........
        DrawText("DVD", (int)textPos.x, (int)textPos.y, 80, textColor); // menggambar tulisan "DVD"
        ........
    }

    return 0;
}
{% endhighlight %}

* Jangan lupa panggil fungsi CloseWindow(void) di penghujung code.
{% highlight cpp %}
#include "raylib.h"

int main()
{
    ........
    ........
    while (!WindowShouldClose())
    {
        ........
        ........
    }

    CloseWindow(); // menutup dan meng-unload window

    return 0;
}
{% endhighlight %}

## Hasil Finishing
{% highlight cpp %}
/*
 .--..--..--..--..--..--..--..--..--..--..--..--..--..--..--..--.
/ .. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \.. \
\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/ /
 \/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /
 / /\/ /`' /`' /`' /`' /`' /`' /`' /`' /`' /`' /`' /`' /`' /\/ /\
/ /\ \/`--'`--'`--'`--'`--'`--'`--'`--'`--'`--'`--'`--'`--'\ \/\ \
\ \/\ \                                                    /\ \/ /
 \/ /\ \                                                  / /\/ /
 / /\/ /           Bouncing DVD                           \ \/ /\
/ /\ \/                                                    \ \/\ \
\ \/\ \                  by Wildan R. (@wildan9)           /\ \/ /
 \/ /\ \                                                  / /\/ /
 / /\/ /                                                  \ \/ /\
/ /\ \/                                                    \ \/\ \
\ \/\ \.--..--..--..--..--..--..--..--..--..--..--..--..--./\ \/ /
 \/ /\/ ../ ../ ../ ../ ../ ../ ../ ../ ../ ../ ../ ../ ../ /\/ /
 / /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\/ /\
/ /\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \/\ \
\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `'\ `' /
*/

#include "raylib.h"

int main()
{
    InitWindow(800, 450, "Bouncing DVD");
    SetTargetFPS(60);

    Vector2 textPos = { GetScreenWidth() / 2.0f, GetScreenHeight() / 2.0f };
    Vector2 speed = { 4.5f, 2.0f };
    Color arrColor[] = { RED, BROWN, YELLOW, GREEN, PINK, BLUE, PURPLE, GOLD };
    Color textColor = BLUE;

    while (!WindowShouldClose())
    {
        BeginDrawing();

            ClearBackground(BLACK);

            textPos.x += speed.x;
            textPos.y += speed.y;

            if (textPos.x >= (GetScreenWidth() - 150.0f) || textPos.x <= 0)
            {
                speed.x *= -1.0f;
                textColor = arrColor[GetRandomValue(0, 8)];
            }
            if (textPos.y >= (GetScreenHeight() - 70.0f) || textPos.y <= 0)
            {
                speed.y *= -1.0f;
                textColor = arrColor[GetRandomValue(0, 8)];
            }

            DrawText("DVD", (int)textPos.x, (int)textPos.y, 80, textColor);

        EndDrawing();
    }

    CloseWindow();

    return 0;
}
{% endhighlight %}

Referensi:<br>
[https://www.raylib.com/cheatsheet/cheatsheet.html](https://www.raylib.com/cheatsheet/cheatsheet.html){:target="\_blank"}
