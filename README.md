# Harjoitustehtavat

ohjelmalista = {}


def tallenna_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str, sali:int):
    ohjelmalista[elokuva] = (kellonaika, sali)
    esitys = (elokuva, kellonaika, sali)
    return esitys
    
    

def onko_elokuva(ohjelmalista:dict, elokuva:str) -> bool:
    if elokuva in ohjelmalista:
        return True
    else:
        return False

def onko_elokuva_kellonaika(ohjelmalista:dict, elokuva:str, kellonaika:str) -> bool: #tarkastaa onko tietty elokuva tiettyyn aikaan ohjelmistossa
    if (elokuva and kellonaika) in ohjelmalista:
        return True
    else:
        return False       
        
def poista_elokuva(ohjelmalista:dict, elokuva:str, kellonaika:str) -> bool:
    if onko_elokuva_kellonaika(ohjelmalista, elokuva, kellonaika):
        del ohjelmalista[elokuva]
        return True
    else:
        return False

def salin_elokuvat(ohjelmalista:dict, sali:int) -> list: #Listataan halutun salin elokuvat
    elokuvalista = []
    arvot = list(ohjelmalista.values())
    for i in arvot:
        if sali in i:
            elokuvalista.append(i)
    return elokuvalista
    
def tulosta_salin_elokuvat(esitys: tuple):
    print(f"Elokuva: {esitys[0]}, Kello: ({esitys[1]}), Sali: {esitys[2]}")



sali_1 = [[1,2,3,4,5,6,7,8],[9,10,11,12,13,14,15,16],[17,18,19,20,21,22,23,24]]
sali_2 = [[1,2,3,4,5,6,7,8],[9,10,11,12,13,14,15,16],[17,18,19,20,21,22,23,24],[25,26,27,28,29,30,31,32],[33,34,35,36,37,38,39,40]]
sali_3 = [[1,2,3,4,5,6,7,8],[9,10,11,12,13,14,15,16],[17,18,19,20,21,22,23,24],[25,26,27,28,29,30,31,32],[33,34,35,36,37,38,39,40],[41,42,43,44,45,46,47,48],[49,50,51,52,53,54,55,56]]


print("Tervetuloa elokuvateatterin varausjärjestelmään.\nValitse käyttötarkoitus.")
print("1: Ylläpitäjä")
print("2: Asiakas")
valinta = int(input("Valinta: "))

if valinta == 1:
    print("----------------------------------------")
    print("Elokuvateatterin varausjärjestelmä")
    print("Valitse:")
    print("1: Lisää elokuva ohjelmistoon")
    print("2: Poista elokuva ohjelmistosta")
    print("3: Listaa ohjelmisto")
    print("0: Poistu")
    print("----------------------------------------")
    valinta = int(input("Valinta: "))

    while valinta != 0:     #Ylläpitäjän käyttöliittymä

        if valinta == 1:
            elokuva = input("Elokuvan nimi: ")
            kellonaika = input("Lisää kellonaika: ")
            sali = input("Salin numero: ")
            tallenna_elokuva(ohjelmalista, elokuva, kellonaika, sali)
        
        elif valinta == 2:
            elokuva = input("Anna elokuvan nimi: ")
            kellonaika = input("Anna kellonaika: ")
            poista_elokuva(ohjelmalista, elokuva, kellonaika)
            print(f"Elokuva {elokuva} kello {kellonaika} poistettu")
        
        elif valinta == 3:
            
            print("Ohjelmalista: ")
            print(ohjelmalista)
            

        print("----------------------------------------")
        print("Elokuvateatterin varausjärjestelmä")
        print("Valitse:")
        print("1: Lisää elokuva ohjelmistoon")
        print("2: Poista elokuva ohjelmistosta")
        print("3: Listaa ohjelmisto")
        print("0: Poistu")
        print("----------------------------------------")
        valinta = int(input("Valinta: "))    

if valinta == 2:
    print("----------------------------------------")
    print("Elokuvateatterin varausjärjestelmä")
    print("Valitse:")
    print("1: Lisää elokuva ohjelmistoon")
    print("2: Poista elokuva ohjelmistosta")
    print("3: Listaa ohjelmisto")
    print("0: Poistu")
    print("----------------------------------------")
    valinta = int(input("Valinta: "))
