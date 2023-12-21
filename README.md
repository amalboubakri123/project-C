#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Définition des structures de données
typedef struct Bus {
    int id;
    char numero[10];
    char type[20];
    int capacite;
    int nombreDePlaceReservees;
} Bus;

typedef struct Voyageur {
    int id;
    char nom[20];
    char prenom[20];
    char dateDeNaissance[11];
    int age;
    int idBus;
    int placeReservee;
} Voyageur;

typedef struct Reservation {
    int id;
    int idVoyageur;
    int idBus;
    char dateDeReservation[11];
    char dureeDeLaReservation[6];
} Reservation;

// Définition des fonctions
void ajouterBus(Bus bus);
void ajouterVoyageur(Voyageur voyageur);
void ajouterReservation(Reservation reservation);
void afficherLesBuses();
void afficherLesVoyageurs();
void afficherLesReservations();

// Définition des constantes
const char* FICHIER_BUS = "bus.dat";
const char* FICHIER_VOYAGEUR = "voyageur.dat";
const char* FICHIER_RESERVATION = "reservation.dat";

int main() {
    // Exemple d'utilisation des fonctions
    Bus bus1 = { 1, "12345", "Autobus", 80, 20 };
    Bus bus2 = { 2, "67890", "Camion", 100, 30 };
    ajouterBus(bus1);
    ajouterBus(bus2);

    Voyageur voyageur1 = { 1, "Alice", "Dupont", "01/01/1990", 35, 1, 1 };
    Voyageur voyageur2 = { 2, "Bob", "Lebghil", "02/02/1985", 30, 2, 2 };
    ajouterVoyageur(voyageur1);
    ajouterVoyageur(voyageur2);

    Reservation reservation1 = { 1, 1, 1, "22/12/2023", "08:00" };
    Reservation reservation2 = { 2, 2, 2, "23/12/2023", "12:00" };
    ajouterReservation(reservation1);
    ajouterReservation(reservation2);

    afficherLesBuses();
    afficherLesVoyageurs();
    afficherLesReservations();

    return 0;
}

void ajouterBus(Bus bus) {
    FILE* fichier = fopen(FICHIER_BUS, "ab");
    fwrite(&bus, sizeof(Bus), 1, fichier);
    fclose(fichier);
}

void ajouterVoyageur(Voyageur voyageur) {
    FILE* fichier = fopen(FICHIER_VOYAGEUR, "ab");
    fwrite(&voyageur, sizeof(Voyageur), 1, fichier);
    fclose(fichier);
}

void ajouterReservation(Reservation reservation) {
    FILE* fichier = fopen(FICHIER_RESERVATION, "ab");
    fwrite(&reservation, sizeof(Reservation), 1, fichier);
    fclose(fichier);
}

void afficherLesBuses() {
    FILE* fichier = fopen(FICHIER_BUS, "rb");
    Bus bus;
    while (fread(&bus, sizeof(Bus), 1, fichier)) {
        printf("%s - %s - %d - %d\n", bus.numero, bus.type, bus.capacite, bus.nombreDePlaceReservees);
    }
    fclose(fichier);
}

void afficherLesVoyageurs() {
    FILE* fichier = fopen(FICHIER_VOYAGEUR, "rb");
    Voyageur voyageur;
    while (fread(&voyageur, sizeof(Voyageur), 1, fichier)) {
        printf("%s %s - %s - %d - %d - %d\n", voyageur.nom, voyageur.prenom, voyageur.dateDeNaissance, voyageur.age, voyageur.idBus, voyageur.placeReservee);
    }
    fclose(fichier);
}

void afficherLesReservations() {
    FILE* fichier = fopen(FICHIER_RESERVATION, "rb");
    Reservation reservation;
    while (fread(&reservation, sizeof(Reservation), 1, fichier)) {
        printf("%d - %d - %d - %s - %s\n", reservation.id, reservation.idVoyageur, reservation.idBus, reservation.dateDeReservation, reservation.dureeDeLaReservation);
    }
    fclose(fichier);
}
