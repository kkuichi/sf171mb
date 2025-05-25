# GPT Detector: Automatická detekcia GPT generovaných textov pomocou metód hlbokého učenia

### Štefan Fečik
    # ŠKOLITEĽ: Ing.~Viera~Krešňáková, PhD.
    # ROK: 2024/2025
    # UNIVERZITA: Technická univerzita v Košiciach
    # FAKULTA: Fakulta Elektrotechniky a Informatiky
    # ŠTUDIJNÝ ODBOR: Informatika
    # ŠTUDIJNÝ PROGRAM: Hospodárska informatika

Tento repozitár obsahuje zdrojové kódy mojej bakalárskej práce zameranej na automatickú detekciu GPT generovaných textov pomocou metód hlbokého učenia.

## Abstrakt

Bakalárska práca sa zameriava na detekciu textov generovaných umelou inteligenciou, konkrétne modelmi typu GPT, a ich odlíšenie od textov napísaných človekom. Cieľom je analyzovať a porovnať výkonnosť vybraných jazykových modelov a klasifikačných prístupov. Praktická časť zahŕňa implementáciu a hodnotenie modelov e5-small-lora, DeepSeek a LLaMA, testovaných rôznymi typmi promptov. Teoretická časť sa venuje základom umelej inteligencie, strojovému a hlbokému učeniu, generatívnym modelom, architektúre transformerov a spracovaniu textu. Práca sa končí zhrnutím poznatkov a návrhmi pre ďalší výskum v oblasti detekcie generovaného obsahu.

---

##  Obsah repozitára

### Úprava datasetov (`/uprava_datasetov`)
- Úprava zdrojového datasetu na potrebný tvar.
- Výsledný súbor na testovanie.

###  Modelové súbory (`/modelfiles`)
- Modelové súbory pre modely LLaMA a DeepSeek.

###  Testovanie (`/testovanie`)
- Testovanie jednotlivých modelov.
- Vyhodnotenie modelov.

###  Výsledné datasety (`/datasety_s_predikciami`)
- Datasety s výslednými predikciami jednotlivých modelov

---

## Požiadavky na spustenie

Na spustenie tohto projektu je potrebné mať lokálne nainštalované jazykové modely LLaMA 3.2 a DeepSeek-R1 prostredníctvom nástroja Ollama.

Modely je potrebné najprv stiahnuť do vlastného zariadenia pomocou nasledujúcich príkazov v príkazovom riadku:
  - ollama run llama3.2
  - ollama run deepseek-r1

Následne je potrebné vytvoriť vlastné varianty modelov s prispôsobenými promptmi alebo systémovými inštrukciami. To sa vykonáva pomocou nasledujúcich príkazov v termináli:
  - ollama create llama_detector1 -f custom_llama1
  - ollama create llama_detector2 -f custom_llama2
  - ollama create llama_detector3 -f custom_llama3
  - ollama create deepseek_detector -f custom_deepseek

Každý príkaz využíva vlastný konfiguračný súbor (Modelfile) umiestnený v príslušnom priečinku, ktorý definuje správanie a parametre daného modelu.

---

###  Dataset

V práci bol použitý verejne dostupný dataset **GPT-wiki-intro** z platformy huggingface, ktorý obsahuje úvodné časti článkov z Wikipédie. 
Tento dataset bol špeciálne pripravený pre úlohu binárnej klasifikácie textov na základe ich pôvodu, či ide o text napísaný človekom alebo generovaný jazykovým modelom GPT.

- [Link na dataset](https://huggingface.co/datasets/aadityaubhat/GPT-wiki-intro)
- Pre spracovanie a testovanie boli texty zjednodušené na binárny formát 0/1.
- Dataset bol upravený len na stĺpce data a label.
- Stĺpec data:
  - Reálne úvodné odseky z Wikipédie (ľudsky písané texty).
  - Texty vygenerované veľkými jazykovými modelmi typu GPT na rovnaké témy.
- Stĺpec label:
  - 0 - napísaný človekom
  - 1 - generovaný umelou inteligenciou
- Na testovanie bola použitá testovacia množina datasetu.


---

###  Použité knižnice

Na spustenie projektu a experimentov sú potrebné nasledujúce knižnice Pythonu:

  - pandas >= 1.5.3 – manipulácia a predspracovanie dát
  - numpy >= 1.24.0 – numerické výpočty a operácie s poľami
  - tqdm >= 4.67.1 – vizualizácia priebehu iterácií
  - scikit-learn >= 1.3.0 – hodnotiace metriky (napr. confusion_matrix, MCC)
  - langchain-ollama >= 0.3.0 – integrácia LLM cez LangChain a Ollama
  - concurrent.futures – paralelné spracovanie pomocou vlákien (štandardná knižnica)
  - re – regulárne výrazy na spracovanie textu (štandardná knižnica)

---
