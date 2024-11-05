#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct osoba {
    char ime[50];
    char prezime[50];
    int godina_rod;
    struct osoba* next;
} Osoba;

Osoba* dodaj_na_pocetak(Osoba* head, const char* ime, const char* prezime, int godina_rod) {
    Osoba* novaOsoba = (Osoba*)malloc(sizeof(Osoba));
    if (novaOsoba == NULL) {
        printf("Error!\n");
        return head;
    }
    strcpy(novaOsoba->ime, ime);
    strcpy(novaOsoba->prezime, prezime);
    novaOsoba->godina_rod = godina_rod;
    novaOsoba->next = head;
    return novaOsoba;
}

Osoba* dodaj_na_kraj(Osoba* head, const char* ime, const char* prezime, int godina_rod) {
    Osoba* novaOsoba = (Osoba*)malloc(sizeof(Osoba));
    if (novaOsoba == NULL) {
        printf("Error!\n");
        return head;
    }
    strcpy(novaOsoba->ime, ime);
    strcpy(novaOsoba->prezime, prezime);
    novaOsoba->godina_rod = godina_rod;
    novaOsoba->next = NULL;

    if (head == NULL) {
        return novaOsoba; 
    }
    else {
        Osoba* trenutna = head;
        while (trenutna->next != NULL) {
            trenutna = trenutna->next;
        }
        trenutna->next = novaOsoba;
    }
    return head;
}

Osoba* dodaj_ispred(Osoba* head, const char* prezime, const char* ime, const char* novo_prezime, int godina_rod) {
    Osoba* novaOsoba = (Osoba*)malloc(sizeof(Osoba));
    if (novaOsoba == NULL) {
        printf("Error!\n");
        return head;
    }
    strcpy(novaOsoba->ime, ime);
    strcpy(novaOsoba->prezime, novo_prezime);
    novaOsoba->godina_rod = godina_rod;

    if (head == NULL || strcmp(head->prezime, prezime) == 0) {
        novaOsoba->next = head;
        return novaOsoba;
    }

    Osoba* trenutna = head;
    while (trenutna->next != NULL && strcmp(trenutna->next->prezime, prezime) != 0) {
        trenutna = trenutna->next;
    }

    if (trenutna->next != NULL) {
        novaOsoba->next = trenutna->next;
        trenutna->next = novaOsoba;
    }
    return head;
}

Osoba* dodaj_iza(Osoba* head, const char* prezime, const char* ime, const char* novo_prezime, int godina_rod) {
    Osoba* trenutna = head;
    while (trenutna != NULL && strcmp(trenutna->prezime, prezime) != 0) {
        trenutna = trenutna->next;
    }
    if (trenutna == NULL) return head;

    Osoba* novaOsoba = (Osoba*)malloc(sizeof(Osoba));
    if (novaOsoba == NULL) {
        printf("Error!\n");
        return head;
    }
    strcpy(novaOsoba->ime, ime);
    strcpy(novaOsoba->prezime, novo_prezime);
    novaOsoba->godina_rod = godina_rod;
    novaOsoba->next = trenutna->next;
    trenutna->next = novaOsoba;

    return head;
}

void spremi_u_datoteku(Osoba* head, const char* filename) {
    FILE* file = fopen(filename, "w");
    if (!file) {
        perror("Greska pri otvaranju datoteke");
        return;
    }

    Osoba* trenutna = head;
    while (trenutna != NULL) {
        fprintf(file, "%s %s %d\n", trenutna->ime, trenutna->prezime, trenutna->godina_rod);
        trenutna = trenutna->next;
    }

    fclose(file);
}

Osoba* ucitaj_iz_datoteke(Osoba* head, const char* filename) {
    FILE* file = fopen(filename, "r");
    if (!file) {
        perror("Greska pri otvaranju datoteke");
        return head;
    }

    char ime[50], prezime[50];
    int godina_rod;

    while (fscanf(file, "%s %s %d", ime, prezime, &godina_rod) == 3) {
        head = dodaj_na_kraj(head, ime, prezime, godina_rod);
    }

    fclose(file);
    return head;
}


void ispisi(Osoba* head) {
    Osoba* trenutna = head;
    while (trenutna != NULL) {
        printf("Ime: %s, Prezime: %s, Godina rodenja: %d\n", trenutna->ime, trenutna->prezime, trenutna->godina_rod);
        trenutna = trenutna->next;
    }
}

Osoba* trazi(Osoba* head, const char* prezime) {
    Osoba* trenutna = head;
    while (trenutna != NULL) {
        if (strcmp(trenutna->prezime, prezime) == 0) {
            return trenutna;
        }
        trenutna = trenutna->next;
    }
    return NULL;
}

Osoba* brisi(Osoba* head, const char* prezime) {
    Osoba* trenutna = head;
    Osoba* prethodna = NULL;

    while (trenutna != NULL && strcmp(trenutna->prezime, prezime) != 0) {
        prethodna = trenutna;
        trenutna = trenutna->next;
    }

    if (trenutna == NULL) {
        printf("Osoba s prezimenom %s nije pronadena.\n", prezime);
        return head;
    }

    if (prethodna == NULL) {
        head = trenutna->next;  
    }
    else {
        prethodna->next = trenutna->next; 
    }

    return head;
}

int main() {
    Osoba* head = NULL;
    int x;
    char ime[50], novo_prezime[50], prezime[50];
    int godina_rod;

    do {
        printf("\nMeni:\n");
        printf("1. Dodaj osobu na pocetak\n");
        printf("2. Dodaj osobu na kraj\n");
        printf("3. Dodaj osobu ispred druge osobe\n");
        printf("4. Dodaj osobu iza druge osobe\n");
        printf("5. Ispisi listu\n");
        printf("6. Pronadi osobu po prezimenu\n");
        printf("7. Obrisi osobu po prezimenu\n");
        printf("8. Spremi listu u datoteku\n");
        printf("9. Ucitaj listu iz datoteke\n");
        printf("0. Izlaz\n");
        printf("Unesite svoj izbor: ");
        scanf("%d", &x);
        getchar();

        switch (x) {
        case 1:
            printf("Unesite ime, prezime i godinu rodenja: ");
            scanf("%s %s %d", ime, prezime, &godina_rod);
            head = dodaj_na_pocetak(head, ime, prezime, godina_rod);
            break;
        case 2:
            printf("Unesite ime, prezime i godinu rodenja: ");
            scanf("%s %s %d", ime, prezime, &godina_rod);
            head = dodaj_na_kraj(head, ime, prezime, godina_rod);
            break;
        case 3:
            printf("Unesite prezime osobe ispred koje dodajete, te ime, prezime i godinu nove osobe: ");
            scanf("%s %s %s %d", prezime, ime, novo_prezime, &godina_rod);
            head = dodaj_ispred(head, prezime, ime, novo_prezime, godina_rod);
            break;
        case 4:
            printf("Unesite prezime osobe iza koje dodajete, te ime, prezime i godinu nove osobe: ");
            scanf("%s %s %s %d", prezime, ime, novo_prezime, &godina_rod);
            head = dodaj_iza(head, prezime, ime, novo_prezime, godina_rod);
            break;
        case 5:
            ispisi(head);
            break;
        case 6: {
            printf("Unesite trazeno prezime: ");
            scanf("%s", prezime);
            Osoba* trazena = trazi(head, prezime);
            if (trazena) {
                printf("%s %s, %d\n", trazena->ime, trazena->prezime, trazena->godina_rod);
            }
            else {
                printf("Osoba s prezimenom %s nije pronadena.\n", prezime);
            }
            break;
        }
        case 7:
            printf("Unesite prezime osobe koju zelite obrisati: ");
            scanf("%s", prezime);
            head = brisi(head, prezime);
            break;
        case 8:
            spremi_u_datoteku(head, "osobe.txt");
            break;
        case 9:
            head = ucitaj_iz_datoteke(head, "osobe.txt");
            break;
        case 0:
            printf("Izlaz iz programa.\n");
            break;
        default:
            printf("Greska!\n");
        }
    } while (x != 0);

    while (head != NULL) {
        Osoba* temp = head;
        head = head->next;
        free(temp);
    }

    return 0;
}
