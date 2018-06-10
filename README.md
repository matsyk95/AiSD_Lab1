#include <iostream>

using namespace std;

class Klasa{
public:
    int wartosc;

    int compareTo(Klasa dwa){
        if(wartosc > dwa.wartosc) return 1;
        if(wartosc < dwa.wartosc) return -1;
        return 0;
    }
};
//funkcja ma scalic dwie tabele arr[l..m] i arr[m+1..r]
void merge(Klasa arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
    Klasa L[n1], R[n2]; //tworzenie tablic tymczasowych
    // L zawiera elementy lewej podtablicy , R prawej
// kopiowanie danych do tych tablic

    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];
// scalanie tablic do arr[l..r]
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i].compareTo(R[j]) <= 0)
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
//kopiowanie pozostalych elementow do L[] jesli takie istnieja
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }
//kopiowanie pozostalych elementow do R[] jesli takie istnieja
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}
// iteracyjna funkcja,  sortuje arr[0..n-1]
void mergeSort(Klasa arr[], int n)
{
   int aktualny_rozmiar; //dla obecnej wielkosci tablicy
   int lewy_start;
//scalanie zastepczej tablicy oddolnie, , Ciąg danych możemy wstępnie podzielić na n serii długości 1, scalić je tak, by otrzymać n/2 serii długości 2, scalić je otrzymując n/4 , serii długości 4
   for (aktualny_rozmiar=1; aktualny_rozmiar<=n-1; aktualny_rozmiar = 2*aktualny_rozmiar)
   {//dodajemy pkt poczatkowy inny od aktualnego
       for (lewy_start=0; lewy_start<n-1; lewy_start += 2*aktualny_rozmiar)
       { //znajdujemy koncowy pkt po lewej czesci tba tymczasowej ,srodek+1
           int srodek = lewy_start + aktualny_rozmiar - 1;
           int prawy_koniec = min(lewy_start + 2*aktualny_rozmiar - 1, n-1);
//scalenie subbarray arr[lewy_start...srodek] i arr[srodek+1...prawy_koniec]
           merge(arr, lewy_start, srodek, prawy_koniec);
       }
   }
}
int main()
{
    Klasa tablica[5];
    tablica[0].wartosc = 20;
    tablica[1].wartosc = 18;
    tablica[2].wartosc = 17;
    tablica[3].wartosc = 15;
    tablica[4].wartosc = 14;

    mergeSort(tablica,4);
    for(int i = 0; i <5; i++)
        cout << tablica[i].wartosc << endl;
}


/*int main()
{
    Klasa tablica[19];
    tablica[0].wartosc = 2;
    tablica[1].wartosc = 10;
    tablica[2].wartosc = 8;
    tablica[3].wartosc = 13;
    tablica[4].wartosc = 27;
    tablica[6].wartosc = 23;
    tablica[7].wartosc = 15;
    tablica[8].wartosc = 82;
    tablica[9].wartosc = 17;
    tablica[10].wartosc = 37;
    tablica[11].wartosc = 130;
    tablica[12].wartosc = 86;
    tablica[13].wartosc = 137;
    tablica[14].wartosc = 273;
    tablica[16].wartosc = 235;
    tablica[17].wartosc = 154;
    tablica[18].wartosc = 825;
    tablica[19].wartosc = 177;
    tablica[20].wartosc = 375;

    mergeSort(tablica,19);
    for(int i = 0; i <20; i++)
        cout << tablica[i].wartosc << endl;
}*/
