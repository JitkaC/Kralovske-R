# Kralovske-R

# Úvod, práce s daty

# JAké balíčky už mám nainstalované?
library()
# Instalace balíčku
install.packages("název_balíčku")
# Načtení balíčku
library("název_balíčku")

# Import dat

# Nastavení pracovní složky (set working directory)
setwd(".../Data")

# nebo

setwd("C:...\\Data")

# Import dat z Excelu

# Balíček "readxl"

# Instalace balíčku
install.packages("readxl")
library("readxl")
#
#
# Práce s listy
#
# Výčet listů v daném excelovském souboru
excel_sheets()
#
# Načtení souboru formátu excel
read_excel() 
excel_sheets("Resources.xlsx")

#
# Chci pracovat s konkrétním sheetem
Jméno_datové_množiny = read_excel("Soubor.xlsx", sheet = "Název_sheetu")
View(Jméno_datové_množiny)
#
# Nevím název sheetuz, vím kolikátý je:
Jméno_datové_množiny = read_excel("Soubor.xlsx", sheet = 2)
View(Jméno_datové_množiny)
#
# Práce s názvy proměnných 
#
# Následující příkaz importuje data z třetího listu souboru Soubor, a R sám nazve sloupce (proměnné)
#
Jméno_datové_množiny = read_excel("Soubor.xlsx", sheet = 3, col_names = FALSE)
View(Jméno_datové_množiny)
#
# Následující příkaz importuje data z třetího listu souboru Soubor, a proměnné nazveme my
#
Jméno_datové_množiny = read_excel("Soubor.xlsx", sheet = 3, col_names = c("Proměnná1", "Proměnná2", "Proměnná3",
"Proměnná4"))​
View(Jméno_datové_množiny)
#
# Někdy jsou v Excelu zbytečný řádky (třeba info o tom kdo data kódoval, datum...), které chceme přeskočit
# Na to použijeme příkaz skip
# Příkaz na řtvrtém sheetu souboru Soubor přeskočí prvních 15 řádků, výsledek se načte do proměnné Jméno_datové_množiny
Jméno_datové_množiny = read_excel("Soubor.xlsx", sheet = 4, skip = 15)

#
# Čištění dat
#
# Smaže všechny řádky (případy) které obsahují chybějící hodnoty NA

Data_clean = na.omit(Data)
# Množina Data_clean obsahuje nahraná data (třeba z nějakého excel sheetu) a uvedený příkaz je vyčistí od chybějících hodnot

# Příkaz pro zachycení všech chybějících hodnot (NA)
is.na(data)

# Jsou nějaký chybějící hodnoty? Měla by vracet T = true nebo F = false
any(is.na(data))

# Všechny prázdný řetězce nahradit NA
data$proměnná[data$proměnná == ""] <- NA
# Někdy je prázdná hodnota prostě "nic", a není kódována jako NA
# Pak je vhodné nastavit ji jako řetězec a pak použít příkaz výše pro nahrazení všech řetězců, které jsou " " (tedy mezera) hodnotou NA

# Chci vidět které případy nemají NA
complete.cases(data)

# Příkaz omit pro smazání všeho co obsahuje missing values - je dobrý nahrát to do nový proměnný, aby nedošlo ke ztrátě dat
na.omit(data)

# Kontrola dat

# Jakou třídu má proměnná? (Kategorická? Numerická? Integer?)
class(Proměnná)

# Co když má proměnná nastavenou špatnou třídu? Přepsat!
Data$Proměnná <- as.character(Data$Proměnná)
# V podstatě říkáme 'proměnné Proměnná ze souboru Data přiřaď třídu character'

# Jaký názvy mají proměnné v souboru?
colnames(Data)

# Prvních 10 a posledních 10 řádků
head(Data, n = 10)
tail(Data, n = 10)

# Explorace hrubých dat s balíčkem psych

# Instalace balíčku

install.packages("psych")
library("psych")

# V balíčku je jednoduchý příkaz na kontrolu struktury dat
describe(bmi_1)

# Histogram
hist(Data$Proměnná)
# Ilustruje rozložení proměnných - je normální?

# Scatterplot
plot(Data$Proměnná1, Data$Proměnná2)
# Scatterplot je třeba provést prakticky vždy, graficky ilustruje vztah mezi proměnnými 

