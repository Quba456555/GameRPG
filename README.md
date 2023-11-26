# GameRPG
import time     # wywołanie modułu z funkcjami do obłsugi czasu, np. time.sleep(0.3) 
import msvcrt   # wywołanie modułu Microsoft Visual C Runtime z funkcjami do obłsugi klawiszy, np. msvcrt.getch()  
import random 
                                   
def zatrzymaj():
    print("Złap 10 świtlików!\nNaciśnij enter")
    msvcrt.getch()
    while not msvcrt.kbhit(): 
        for i in range(1,11):
            print(i)
            time.sleep(0.1)
            if msvcrt.kbhit():
                return i    

def kasyno(zloto):
    while True:
        print("Kasyno. Co chcesz zrobić?")
         time.sleep(0.1)
        print("(1) Graj")
         time.sleep(0.1)
        print("(2) Zakończ")

        if wybor == "1":
            zmiana_zlota = random.randint(-10, 10)
            zloto += zmiana_zlota
            if zmiana_zlota > 0:
                print(f"\nWygrałeś {zmiana_zlota} sztuk złota. Masz teraz {zloto} złota\n")
            else:
                print(f"\nPrzegrałeś {zmiana_zlota} sztuk złota. Masz teraz {zloto} złota\n")
        elif wybor == "2":
            print("Zakończono grę w kasynie.")
            break
        else:
            print("Nieprawidłowy wybór. Wybierz 1 lub 2.")
            time.sleep(0.1)

    return zloto

def spotkanie():
    while True:
        print("Spotkanie z nieznaną postacią... Możesz zyskać manę od 10 do 50. Naciśnij klawisz")
        msvcrt.getch()
        dodaj_many = random.randint(10, 50)
        print(f"Twoja mana wynosi teraz {dodaj_many}. Czy szukasz kolejnego spotkania? (Naciśnij 't' aby losować ponownie)")
        time.sleep(0.1)
        wybor = msvcrt.getch()  # Konwertuj do małych liter dla jednolitości
        if wybor == 't':
            continue  # Ponowne losowanie
        else:
            break  # Zakończenie funkcji
    return dodaj_many

def losuj_przeciwnika(poziom):
    if poziom <= 3:
        ciezki = "Gruby wolny, ale silny"
        sredni = "Średnio szybki i silny"
        lekki = "Chudy słaby, ale szybki"
        przeciwnik = random.choice([ciezki, sredni, lekki])
    else:
        czarownik = "Czarownik"
        troll = "Troll"
        elf = "Elf"
        przeciwnik = random.choice([czarownik, troll, elf])
    return przeciwnik

def wybierz_taktyke():
    while True:
        print("Wybierz taktykę:\n(1) Atak frontalny\n(2) Atak z flanki\n(3) Ataki z ukrycia\n")
        time.sleep(0.1)
        wybor_taktyki = input("Twój wybór: ")
        if 1 <= int(wybor_taktyki) <= 3:
            break
        print("Podaj liczbę z zakresu 1-3.")
        time.sleep(0.1)
    return int(wybor_taktyki)

def walka(taktyka_gracza, przeciwnik):
    print(f"\nWalczyłeś z {przeciwnik}!")
    wynik_walki = random.randint(1, 5) 
    modifier = random.randint(-2, 2)

    if taktyka_gracza == 1:  # Atak frontalny
        wynik_walki += 2
    elif taktyka_gracza == 2:  # Atak z flanki
        wynik_walki += modifier
    elif taktyka_gracza == 3:  # Ataki z ukrycia
        wynik_walki += 1

    return wynik_walki

def sklep(zloto, mana):

    ilosc_many_str = input("Ile many chcesz kupić? 1 złoto= 1 mana (Wpisz 0, aby zakończyć zakupy): ")

    if not ilosc_many_str.isdigit():
        print("Wprowadź liczbę całkowitą.")

    ilosc_many = int(ilosc_many_str)
    cena = ilosc_many

    if cena > zloto:
        print("Nie masz wystarczająco złota. Spróbuj mniejszą ilość.")
    else:
        mana += ilosc_many
        zloto -= cena
        print(f"Kupiłeś {ilosc_many} many za {cena} złota.")
        time.sleep(0.1)
    return zloto, mana

def walka_z_bossem(mana):
    print("Walczysz z bossem 1!")
    time.sleep(0.1)

    zycie_bossa = 60
    strzal_min = 10
    strzal_max = 20

    while mana >= 0:
        print(f"\nAktualne życie bossa 1: {zycie_bossa}")
        time.sleep(0.1)
        print(f"Aktualna ilość many: {mana}")
        time.sleep(0.1)
        input("Naciśnij enter, aby strzelić...\n")

        strzal = random.randint(strzal_min, strzal_max)
        print(f"Zadajesz {strzal} obrażeń bossowi 1!")
        time.sleep(1)

        zycie_bossa -= strzal
        mana -= 10
        print(f"Zostało Ci {mana} many.")
        time.sleep(1)

        if zycie_bossa <= 0:
            print("\nPokonałeś bossa 1! Gratulacje! Idziesz dalej!\n")
            time.sleep(1)
            break

        print("\nBoss 1 kontratakuje!")
        time.sleep(1)
        obrazenia_bossa = random.randint(5, 10)
        print(f"Boss 1 zużył {obrazenia_bossa} Twojej many!")
        time.sleep(1)

        if mana <= obrazenia_bossa:
            print("Za mało many, aby kontynuować walkę!")
            break

        mana -= obrazenia_bossa

    if zycie_bossa > 0:
        print("Niestety, Twoja mana się wyczerpała, nie udało się pokonać tego bossa. Uciekasz.\n")
        time.sleep(1)
    
def walka_z_bossem2(nowa_mana):
    zycie_bossa = 120
    zycie_gracza = 100
    
    print("\nFinałowa walka z potężnym bossem!\n")
    time.sleep(1)
    
    while zycie_bossa > 0 and nowa_mana >= 0 and zycie_gracza > 0:
        time.sleep(1)
        print(f"Aktualne życie bossa: {zycie_bossa}")
        print(f"Aktualne życie gracza: {zycie_gracza}")
        print(f"Aktualna ilość many gracza: {nowa_mana}\n")
        time.sleep(1)
       
        print("Wybierz akcję:")
        print("1. Atak mocny - zużywa 10 many, może zdać 15-25 obrażeń bossowi")
        print("2. Atak słaby - zużywa 5 many, może zadać 10-20 obrażeń bossowi")
        wybor = input("Twój wybór: ")
        
        if wybor == '1':
            strzal = random.randint(15, 25)  # Wynik ataku od 15 do 25
            zycie_bossa -= strzal
            nowa_mana -= 10
            print(f"Tracisz 10 many. Zadałeś bossowi {strzal} obrażeń!\n")
            time.sleep(1)
        elif wybor == '2':
            strzal = random.randint(10, 20)  # Wynik ataku od 15 do 25
            zycie_bossa -= strzal
            nowa_mana -= 5
            print(f"Tracisz 5 many. Zadałeś bossowi {strzal} obrażeń!\n")
            time.sleep(1)
        else:
            print("Nieprawidłowy wybór. Spróbuj ponownie.\n")
            continue
        
        trafienie_krytyczne = random.choice([True, False])  # Sprawdzanie czy dodakowo trafienie krytyczne: 50% szans
        if trafienie_krytyczne:
            obrazenia_krytyczne = random.randint(5, 10)
            zycie_bossa -= obrazenia_krytyczne
            print(f"Dodatkowo trafienie krytyczne! Zadałeś bossowi dodatkowe {obrazenia_krytyczne} obrażeń!\n")
            time.sleep(1)

        # Symulacja ataku bossa
        if zycie_bossa > 0:
            print("\nBoss atakuje!")
            time.sleep(1)
            unik = random.choice([True, False])  # Szansa na unik: 50%
            if unik:
                print("Udało ci się uniknąć ataku bossa!\n")
                time.sleep(1)
            else:
                obrazenia_bossa = random.randint(10, 20)
                zycie_gracza -= obrazenia_bossa
                print(f"Boss zadał Ci {obrazenia_bossa} obrażeń!\n")
                time.sleep(1)
    
    if nowa_mana <= 0:
        print("Nie masz już many. Nie udało Ci się pokonać bossa. Uciekasz!")

    if zycie_bossa <= 0:
        print("Brawo! Pokonałeś potężnego bossa!")
    elif zycie_gracza <= 0:
     time.sleep(0.1)
        print("Przegrałeś walkę z bossem. Twoje życie spadło poniżej zera.")

def logika_gry():
          
    poziom = 1
    wygrane_poziomy = 0
    zdrowie = 10
    zloto = 50
    mana = 0

    print("\nWygraj 5 poziomów aby przejść dalej!\n")

    while wygrane_poziomy < 5:
        przeciwnik = losuj_przeciwnika(poziom)
        print(f"Walczysz na poziomie {poziom} z {przeciwnik}!")
        
        taktyka_gracza = wybierz_taktyke()
        wynik_walki = walka(taktyka_gracza, przeciwnik)
        print(f"Walka wygrana gdy jej wynik większy od 5.\nWynik walki: {wynik_walki}")

        if wynik_walki >= 5:
                wygrane_poziomy += 1
                poziom += 1
                zdrowie += 2
                if zdrowie > 10:
                    zdrowie = 10
                print(f"Pokonałeś przeciwnika! Twoje zdrowie {zdrowie}. Wygrane poziomy {wygrane_poziomy}\n\n")
        else:
            zdrowie -= 2
            wygrane_poziomy -= 1
            if wygrane_poziomy < 1:
                wygrane_poziomy == 0
            print(f"Przegrałeś walkę. Twoje zdrowie {zdrowie}. Wygrane poziomy {wygrane_poziomy}. Spróbuj ponownie.\n")
            if zdrowie <= 0:
                print("Straciłeś wszystkie punkty zdrowia. Koniec gry.")
                break
        
        if wygrane_poziomy == 5:
            wygrane_poziomy += 1
            print("Wygrałeś wszystkie walki!\n")

    print(f"Masz teraz {zloto} sztuk złota. Idziesz do kasyna")
     time.sleep(0.1)
    zloto = kasyno(50)
    print(f"Masz teraz {zloto} sztuk złota.\n")

    print(f"Masz teraz {mana} many.")
    mana = spotkanie()
    print(f"Twoja mana wynosi teraz {mana}.\n")
    
    print(f"Wchodzisz do sklepu, możesz dokupć many do walki z bossem. Teraz mana {mana}, złoto {zloto}.\n")
    zloto, mana = sklep(zloto, mana)
    print(f"Twoja mana wynosi teraz {mana}, a złoto {zloto}.\n")

    walka_z_bossem(mana)

    print("Złap max 10 magicznych świtlików. To kluczowe aby zwiększyć manę przed walką z Bossem 2!")
    wynik = zatrzymaj()
    nowa_mana = wynik*10
    print(f'Złapałeś {wynik} magicznych świetlików. Twoja nowa mana {wynik}*10={nowa_mana}')
    time.sleep(1)

    walka_z_bossem2(nowa_mana)

logika_gry()
 time.sleep(0.1)
  time.sleep(0.1)
   time.sleep(0.1)
    time.sleep(0.1)
     time.sleep(0.1)
      time.sleep(0.1)
