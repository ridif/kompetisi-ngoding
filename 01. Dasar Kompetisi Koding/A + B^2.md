# A + B^2

| Nama 					| Nilai        	|
| ------------- | ------------- |
| Input file:   | aplusbb.in    |
| Output file:  | aplusbb.out 	|
| Time limit:   | 2 seconds 		|
| Memory limit: | 256 megabytes |

Diberikan dua nilai bertipe integer, A dan B. Output yang dihasilkan adalah A + B<sup>2</sup>

### Input
File input mengandung satu baris dengan 2 nilai integer, A dan B (-10<sup>9</sup> <= A, B <= 10<sup>9</sup>), dipisahkan dengan satu spasi

### Output
Output berupa satu baris hasil dari A + B<sup>2</sup> di file output.

### Contoh
| aplusb.in			| aplusb.out   	|
| ------------- | ------------- |
| 23 11					| 144						|

### Solusi
Problem ini sebenarnya cukup sederhana jika dilihat aturannya. Hanya **menjumlahkan nilai A dengan hasil perpangkatan 2 dari B**. Namun umumnya programmer pemula dalam kontes ngoding kurang memperhatikan batasan suatu tipe data sehingga kasus sederhana ini tergolong _tricky_ dan menyebabkan percobaan/submission jadi banyak. **Ingat, selalu perhatikan batasan input/output!**

Bayangkan salah satu *test case* dengan nilai input berupa batasan maksimum:
10<sup>9</sup> + (10<sup>9</sup>)<sup>2</sup> = 10<sup>9</sup> + 10<sup>18</sup> = 1000000001000000000
Output di atas melebihi daripada batasan maksimum dari suatu integer yang berukuran 32-bit atau 2<sup>31</sup> - 1 = 2147483647. Namun masih mampu ditampung oleh tipe data berukuran 64-bit, karena 2<sup>31</sup> - 1 > 9.2x10<sup>18</sup>. Jadi, kita membutuhkan integer berukuran 64-bit (```long long``` pada C++ dan ```long``` pada Java)

#### Contoh Wrong Answer (WA)
Wrong Answer di C++ yang menggunakan ```int``` untuk semua komputasi.

```cpp
#ifdef JUDGE
#include <fstream>
std::ifstream cin("aplusbb.in");
std::ofstream cout("aplusbb.out");
#else
#include <iostream>
using std::cin;
using std::cout;
#endif

int main() {
	int a, b;
	cin >> a >> b;
	cout << a + b * b;
	return 0;
}
```

Wrong Answer lain di C++. Kita sudah mengganti tipe data output ke ```long long``` namun tidak ada perubahan. Kenapa?

**Perhatikan!** Nilai dari b * b tetap dikomputasi dengan ```int```.
```cpp
#ifdef JUDGE
#include <fstream>
std::ifstream cin("aplusbb.in");
std::ofstream cout("aplusbb.out");
#else
#include <iostream>
using std::cin;
using std::cout;
#endif

int main() {
	int a, b;
	cin >> a >> b;
	long long c = a + b * b;
	cout << c;
	return 0;
	}
```

Wrong Answer di Java. Ketika kita menggunakan fungsi ```Math.pow``` sehingga memudahkan dalam menghitung B<sup>2</sup>, yang terjadi adalah WA karena hasil dari ```Math.pow``` bertipe ```double```, sehingga kehilangan presisi nilai ketika dicast ke ```long```.
```java
import java.io.*;
import java.util.*;

public class Main {
static BufferedReader newInput() throws IOException {
if (System.getProperty("JUDGE") != null) {
return new BufferedReader(new FileReader("aplusbb.in");
} else {
return new BufferedReader(new InputStreamReader(System.in));
}
}

static PrintWriter newOutput() throws IOException {
if (System.getProperty("JUDGE") != null) {
return new PrintWriter("aplusbb.out");
} else {
return new PrintWriter(System.out);
}
}

public static void main(String[] args) throws IOException {
try (BufferedReader in = newInput(); PrintWriter out = newOutput()) {
StringTokenizer tok = new StringTokenizer(in.readLine());
int a = Integer.parseInt(tok.nextToken());
int b = Integer.parseInt(tok.nextToken());
out.println(a + (long) Math.pow(b,2));
}
}
}
```


#### Accepted, C++
Solusi yang benar adalah lakukan _cast_ ke salah satu angka yang digunakan dalam perkalian ke ```long long``` sebelum melakukan perkalian.
```cpp
#ifdef JUDGE
#include <fstream>
std::ifstream cin("aplusbb.in");
std::ofstream cout("aplusbb.out");
#else
#include <iostream>
using std::cin;
using std::cout;
#endif

int main() {
	int a, b;
	cin >> a >> b;
	cout << a + (long long) (b) * b;
	return 0;
}
```

#### Accepted, Java
Berikut solusi yang benar pada Java. Sebagai catatan, Java ```long``` selalu integer berukuran 64-bit, tidak seperti C dan C++.

```java
import java.io.*;
import java.util.*;

public class Main {
	static BufferedReader newInput() throws IOException {
		if (System.getProperty("JUDGE") != null) {
			return new BufferedReader(new FileReader("aplusbb.in");
		} else {
			return new BufferedReader(new InputStreamReader(System.in));
		}
	}

	static PrintWriter newOutput() throws IOException {
		if (System.getProperty("JUDGE") != null) {
			return new PrintWriter("aplusbb.out");
		} else {
			return new PrintWriter(System.out);
		}
	}

	public static void main(String[] args) throws IOException {
		try (BufferedReader in = newInput(); PrintWriter out = newOutput()) {
			StringTokenizer tok = new StringTokenizer(in.readLine());
			int a = Integer.parseInt(tok.nextToken());
			int b = Integer.parseInt(tok.nextToken());
			out.println(a + (long) (b) * b);
		}
	}
}
```
