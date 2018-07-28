# smile
#include <iostream>
#include <conio.h>
using namespace std;

const int SIZE = 10;

struct {
	char item[40];//имя товара
	double price;//цена товара
	int k;//кол-во товара

}invt[SIZE];

void init_m();
char menu();
void enter();
void input(int i);
void display();
void update();

int main() {
	setlocale(0, "RUS");
	char choice;
	init_m();
	for (;;) {
		choice = menu();
		switch (choice) {
		case 'e': enter();
			break;
		case 'd': display();
			break;
		case 'u': update();
			break;
		case 'q': return 0;
		default: break;
		}
	}


	_getch();
}

void init_m() {
	for (int i = 0; i < SIZE; i++) *invt[i].item = '\0';
}

char menu() {
	char ch;
	cout << '\n';
	do {
		cout << "(E)nter(ввести новый элемент)\n";
		cout << "(D)isplay(отобразить всю ведомость)\n";
		cout << "(U)pdate(изменить элементы)\n";
		cout << "(Q)uit(выйти)\n";
		cin >> ch;

	} while (!strchr("eduq", tolower(ch)));
	return ch;
}

void enter() {
	int i;
	for (i = 0; i < SIZE; i++) if (!*invt[i].item) break;

	if (i == SIZE) { cout << "Список полон\n"; return; }

	input(i);


}
void input(int i) {
	cout << "Введите наименование товара: "; cin >> invt[i].item;
	cout << "Введите цену товара: "; cin >> invt[i].price;
	cout << "Введите кол-во товара: "; cin >> invt[i].k;
}

void display() {
	for (int i = 0; *invt[i].item; i++) {
		cout << "(" << i+1 << ")" << endl;
		cout <<"Товар: "<< invt[i].item << endl;
		cout <<"Цена: " << invt[i].price << endl;
		cout <<"Количество: " << invt[i].k << endl;
	}

}

void update() {
	char ch[40];
	cout << "Введите наименование товар: ";
	cin >> ch;
	int i;
	for (i = 0; i < SIZE; i++) if (strchr(ch, *invt[i].item)) break;
	if (i == SIZE) return;
	input(i);
}
