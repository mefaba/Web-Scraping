https://nbviewer.jupyter.org/github/mefaba/Web-Scraping/blob/master/TripAd_thingstodo%20v3.ipynb

```python
import unittest
import time
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from bs4 import BeautifulSoup
import requests
```


```python
chrome_options = webdriver.ChromeOptions()
chrome_options.add_argument("--incognito")
chrome_options.add_argument("--disable-popup-blocking")
browser = webdriver.Chrome("C:\Program Files (x86)\Google\Chrome\Application\chromedriver")
browser.get("https://www.tripadvisor.com/")#,options = chrome_options
```


```python
city_list = ["Singapore","Vancouver", "London", "Toronto", "Budapest", "Hong Kong", "Stockholm", "Sydney", "Kuala Lumpur", "Barcelona", "Paris", "Berlin", "Ottawa", "Melbourne", "Zurich", "Oslo", "Helsinki", "São Paulo", "Hamburg", "Milano"]
```


```python
city_things_dict={} 

for search_key in city_list:
    browser.get("https://www.tripadvisor.com/")
    searcher = browser.find_element_by_xpath("//span[@class='ui_column is-4-mobile brand-quick-links-QuickLinkTileItem__quickLinkTileItem--zKAkR brand-quick-links-QuickLinkTileItem__customizedColForTablet--1ql_j brand-quick-links-commonStyles__order-attractions--2jENs']//a[@class='brand-quick-links-QuickLinkTileItem__link--1k5lE']")
    browser.execute_script("arguments[0].click();", searcher)
    print("clicked to the button")
    searcher = browser.find_element_by_xpath("//input[@placeholder='Where to?']")
    print("hidden butona erişildi")

    searcher.send_keys(search_key) #aramaya istanbul yazdık.
    print("hidden butona istanbul yazıldı")
    time.sleep(2)

    searcher.send_keys(Keys.ENTER) #enter
    time.sleep(5)

    current_url =browser.current_url
    print(current_url)
    current_url =browser.current_url
    url1= requests.get(current_url)   
    try:
        soup = BeautifulSoup(url1.content, 'lxml') 
        elements = soup.find_all(attrs={"class":"attractions-attraction-overview-pills-Pill__pill--1WZY6"})
        list_type_things_to_do = []
        for every in elements:
            list_type_things_to_do.append(every.text)

        city_things_dict[search_key] = list_type_things_to_do
    except:
        print(error)
        city_things_dict[search_key] = "error"
    #for city in city_list:
    #    city_name_cc_dict={}
    #    city_name_cc_dict[city]=cc_list
browser.quit()
print("scraping is finished")
```

    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g294265-Activities-Singapore.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g154943-Activities-Vancouver_British_Columbia.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g186338-Activities-London_England.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g155019-Activities-Toronto_Ontario.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g274887-Activities-Budapest_Central_Hungary.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g294217-Activities-Hong_Kong.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g189852-Activities-Stockholm.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g255060-Activities-Sydney_New_South_Wales.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g298570-Activities-Kuala_Lumpur_Wilayah_Persekutuan.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g187497-Activities-Barcelona_Catalonia.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g187147-Activities-Paris_Ile_de_France.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g187323-Activities-Berlin.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g155004-Activities-Ottawa_Ontario.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g255100-Activities-Melbourne_Victoria.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g188113-Activities-Zurich.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g190479-Activities-Oslo_Eastern_Norway.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g189934-Activities-Helsinki_Uusimaa.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g303631-Activities-Sao_Paulo_State_of_Sao_Paulo.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g187331-Activities-Hamburg.html
    clicked to the button
    hidden butona erişildi
    hidden butona istanbul yazıldı
    https://www.tripadvisor.com/Attractions-g187849-Activities-Milan_Lombardy.html
    scraping is finished
    


```python
city_things_dict
```




    {'Singapore': ['Shopping (492)',
      'Spas & Wellness (453)',
      'Sights & Landmarks (327)',
      'Tours (276)',
      'Outdoor Activities (195)',
      'Fun & Games (190)',
      'Nightlife (171)',
      'Museums (126)',
      'Transportation (124)',
      'Classes & Workshops (124)',
      'Nature & Parks (121)',
      'Food & Drink (116)',
      'Boat Tours & Water Sports (74)',
      'Concerts & Shows (44)',
      'Events (21)',
      'See all',
      'Central Area/City Area (1,038)',
      'Downtown Core/Downtown Singapore (288)',
      'Central Business District (194)',
      'Rochor (187)',
      'Orchard (182)',
      'Outram (179)',
      'Orchard Road (177)',
      'Chinatown (133)',
      'Colonial District/Civic District (106)',
      'Marina Bay (105)',
      'Boulevard (103)',
      'Singapore River/Riverside (102)',
      'Bukit Merah (94)',
      'Kallang (91)',
      'City Hall (82)',
      'See all',
      'Good for a Rainy Day (382)',
      'Free Entry (372)',
      'Budget-friendly (276)',
      'Good for Couples (259)',
      'Good for Big Groups (229)',
      'Good for Kids (211)',
      'Hidden Gems (80)',
      'Honeymoon spot (58)',
      'Good for Adrenaline Seekers (48)',
      'Adventurous (30)'],
     'Vancouver': ['Spas & Wellness (224)',
      'Tours (216)',
      'Outdoor Activities (178)',
      'Shopping (157)',
      'Sights & Landmarks (106)',
      'Nightlife (92)',
      'Food & Drink (70)',
      'Boat Tours & Water Sports (67)',
      'Museums (66)',
      'Nature & Parks (61)',
      'Fun & Games (56)',
      'Transportation (52)',
      'Concerts & Shows (51)',
      'Classes & Workshops (24)',
      'Day Trips (19)',
      'See all',
      'Central (457)',
      'Downtown (356)',
      'East Vancouver (145)',
      'False Creek (113)',
      'Fairview (113)',
      'Granville Street (88)',
      'Granville Island & Fairview (77)',
      'West End (76)',
      'Robson Street (74)',
      'Kitsilano (72)',
      'Coal Harbour (70)',
      'Yaletown & False Creek North (69)',
      'Gastown (66)',
      'Granville Island (59)',
      'Yaletown (51)',
      'See all',
      'Good for Couples (221)',
      'Good for a Rainy Day (186)',
      'Budget-friendly (156)',
      'Good for Big Groups (144)',
      'Free Entry (125)',
      'Good for Kids (109)',
      'Hidden Gems (54)',
      'Honeymoon spot (53)',
      'Good for Adrenaline Seekers (46)',
      'Adventurous (28)'],
     'London': ['Nightlife (1,223)',
      'Tours (1,034)',
      'Sights & Landmarks (977)',
      'Shopping (938)',
      'Spas & Wellness (790)',
      'Fun & Games (526)',
      'Concerts & Shows (420)',
      'Museums (410)',
      'Transportation (407)',
      'Outdoor Activities (298)',
      'Food & Drink (296)',
      'Classes & Workshops (293)',
      'Nature & Parks (257)',
      'Boat Tours & Water Sports (93)',
      'Day Trips (65)',
      'See all',
      'Soho (262)',
      'City of London (261)',
      'Mayfair (225)',
      'Covent Garden (211)',
      'Westminster (163)',
      'Trafalgar Square / Embankment (139)',
      'Marylebone (134)',
      'Bloomsbury (121)',
      'Southwark (113)',
      'Notting Hill (106)',
      'Holborn (105)',
      'Shoreditch (98)',
      'Chelsea (94)',
      'Fitzrovia (86)',
      "St. James's (84)",
      'See all',
      'Good for a Rainy Day (1,650)',
      'Good for Couples (1,351)',
      'Free Entry (1,123)',
      'Budget-friendly (938)',
      'Good for Big Groups (921)',
      'Good for Kids (537)',
      'Hidden Gems (521)',
      'Adventurous (175)',
      'Honeymoon spot (147)',
      'Good for Adrenaline Seekers (124)'],
     'Toronto': ['Spas & Wellness (334)',
      'Shopping (238)',
      'Nightlife (207)',
      'Tours (203)',
      'Fun & Games (184)',
      'Sights & Landmarks (181)',
      'Outdoor Activities (146)',
      'Nature & Parks (114)',
      'Museums (110)',
      'Concerts & Shows (97)',
      'Food & Drink (72)',
      'Transportation (70)',
      'Classes & Workshops (58)',
      'Boat Tours & Water Sports (47)',
      'Day Trips (26)',
      'See all',
      'Old Toronto (1,089)',
      'Downtown (639)',
      'Waterfront Communities-The Island (225)',
      'Downtown West (200)',
      'Midtown (167)',
      'West End (130)',
      'Entertainment District (126)',
      'North York (126)',
      'Etobicoke (116)',
      'East End (111)',
      'Church-Yonge Corridor (103)',
      'Bay Street Corridor (98)',
      'Annex (87)',
      'Scarborough (86)',
      'Kensington-Chinatown (66)',
      'See all',
      'Good for a Rainy Day (269)',
      'Good for Couples (269)',
      'Good for Big Groups (211)',
      'Budget-friendly (170)',
      'Free Entry (165)',
      'Good for Kids (120)',
      'Hidden Gems (64)',
      'Honeymoon spot (52)',
      'Good for Adrenaline Seekers (43)',
      'Adventurous (33)'],
     'Budapest': ['Tours (427)',
      'Sights & Landmarks (330)',
      'Nightlife (281)',
      'Shopping (263)',
      'Fun & Games (201)',
      'Outdoor Activities (150)',
      'Spas & Wellness (141)',
      'Museums (135)',
      'Food & Drink (131)',
      'Transportation (79)',
      'Concerts & Shows (61)',
      'Nature & Parks (43)',
      'Classes & Workshops (41)',
      'Boat Tours & Water Sports (37)',
      'Traveler Resources (7)',
      'See all',
      'District V / Inner City (297)',
      'District VII / Jewish Quarter (194)',
      'District I / Buda (147)',
      'Várkerület (33)',
      'Gellert Hill (30)',
      'Belváros-Lipótváros (18)',
      'Terézváros (13)',
      'Margaret Island (8)',
      'Erzsébetváros (7)',
      'Óbuda-Békásmegyer (6)',
      'Zugló (5)',
      'Kispest (5)',
      'Andrássy út (4)',
      'Városliget (4)',
      'Sasad (3)',
      'See all',
      'Good for a Rainy Day (335)',
      'Good for Couples (330)',
      'Budget-friendly (313)',
      'Good for Big Groups (281)',
      'Free Entry (183)',
      'Good for Kids (171)',
      'Hidden Gems (124)',
      'Honeymoon spot (95)',
      'Good for Adrenaline Seekers (70)',
      'Adventurous (47)'],
     'Hong Kong': ['Shopping (485)',
      'Sights & Landmarks (350)',
      'Tours (251)',
      'Outdoor Activities (195)',
      'Nature & Parks (174)',
      'Spas & Wellness (145)',
      'Museums (112)',
      'Fun & Games (100)',
      'Nightlife (96)',
      'Food & Drink (91)',
      'Classes & Workshops (69)',
      'Boat Tours & Water Sports (67)',
      'Transportation (48)',
      'Concerts & Shows (23)',
      'Events (18)',
      'See all',
      'Hong Kong Island (436)',
      'Kowloon (242)',
      'New Territories (232)',
      'Central District (224)',
      'Yau Tsim Mong District (171)',
      'Central (135)',
      'Tsim Sha Tsui (95)',
      'Southern District (50)',
      'Islands District (50)',
      'Sheung Wan (49)',
      'Mong Kok (39)',
      'Eastern District (36)',
      'Sai Kung (35)',
      'Yuen Long (34)',
      'Sha Tin (34)',
      'See all',
      'Free Entry (381)',
      'Budget-friendly (257)',
      'Good for a Rainy Day (252)',
      'Good for Couples (234)',
      'Good for Kids (203)',
      'Good for Big Groups (134)',
      'Hidden Gems (57)',
      'Honeymoon spot (40)',
      'Good for Adrenaline Seekers (22)',
      'Adventurous (14)'],
     'Stockholm': ['Tours (140)',
      'Sights & Landmarks (119)',
      'Outdoor Activities (101)',
      'Shopping (86)',
      'Museums (77)',
      'Fun & Games (64)',
      'Nature & Parks (60)',
      'Boat Tours & Water Sports (50)',
      'Nightlife (40)',
      'Spas & Wellness (39)',
      'Concerts & Shows (28)',
      'Transportation (21)',
      'Food & Drink (21)',
      'Classes & Workshops (10)',
      'Traveler Resources (9)',
      'See all',
      'Norrmalm (120)',
      'Sodermalm Borough (87)',
      'Sodermalm (82)',
      'Gamla Stan & Riddarholmen (80)',
      'Ostermalm (78)',
      'Kungsholmen (32)',
      'Vasastan (32)',
      'Djurgarden & Djurgardsbrunn (32)',
      'SoFo & Medborgarplatsen (25)',
      'Enskede-Arsta-Vantor Borough (20)',
      'Mariatorget (16)',
      'Hornstull & Langholmen (13)',
      'Johanneshov (10)',
      'Slussen (10)',
      'Skeppsholmen (8)',
      'See all',
      'Good for a Rainy Day (141)',
      'Budget-friendly (127)',
      'Good for Couples (114)',
      'Good for Kids (82)',
      'Free Entry (80)',
      'Good for Big Groups (79)',
      'Hidden Gems (36)',
      'Honeymoon spot (30)',
      'Good for Adrenaline Seekers (17)',
      'Adventurous (16)'],
     'Sydney': ['Tours (510)',
      'Outdoor Activities (336)',
      'Spas & Wellness (282)',
      'Nightlife (218)',
      'Shopping (214)',
      'Sights & Landmarks (187)',
      'Boat Tours & Water Sports (152)',
      'Nature & Parks (143)',
      'Food & Drink (130)',
      'Fun & Games (128)',
      'Transportation (110)',
      'Museums (99)',
      'Concerts & Shows (57)',
      'Classes & Workshops (57)',
      'Day Trips (37)',
      'See all',
      'Central Business District (367)',
      'The Rocks (81)',
      'Surry Hills (60)',
      'Darlinghurst (53)',
      'Paddington (46)',
      'Darling Harbour (44)',
      'Newtown (43)',
      'Balmain (30)',
      'Double Bay (26)',
      'Chinatown (21)',
      'Glebe (18)',
      'Inner West (12)',
      'Inner East (11)',
      'Manly (10)',
      'Mosman (10)',
      'See all',
      'Good for Big Groups (348)',
      'Good for Couples (334)',
      'Good for a Rainy Day (277)',
      'Budget-friendly (274)',
      'Free Entry (255)',
      'Good for Kids (187)',
      'Honeymoon spot (90)',
      'Hidden Gems (87)',
      'Good for Adrenaline Seekers (74)',
      'Adventurous (64)'],
     'Kuala Lumpur': ['Tours (193)',
      'Shopping (155)',
      'Spas & Wellness (147)',
      'Transportation (137)',
      'Sights & Landmarks (106)',
      'Outdoor Activities (95)',
      'Nightlife (93)',
      'Day Trips (76)',
      'Fun & Games (65)',
      'Museums (53)',
      'Food & Drink (47)',
      'Classes & Workshops (46)',
      'Nature & Parks (35)',
      'Concerts & Shows (18)',
      'Boat Tours & Water Sports (14)',
      'See all',
      'Good for a Rainy Day (188)',
      'Free Entry (154)',
      'Budget-friendly (150)',
      'Good for Couples (149)',
      'Good for Big Groups (130)',
      'Good for Kids (119)',
      'Hidden Gems (29)',
      'Honeymoon spot (26)',
      'Good for Adrenaline Seekers (24)',
      'Adventurous (14)'],
     'Barcelona': ['Tours (823)',
      'Nightlife (594)',
      'Spas & Wellness (560)',
      'Sights & Landmarks (511)',
      'Outdoor Activities (443)',
      'Shopping (426)',
      'Food & Drink (256)',
      'Fun & Games (210)',
      'Museums (165)',
      'Classes & Workshops (150)',
      'Boat Tours & Water Sports (126)',
      'Transportation (118)',
      'Concerts & Shows (116)',
      'Nature & Parks (115)',
      'Day Trips (63)',
      'See all',
      'Ciutat Vella (Old Town) (956)',
      'Eixample (742)',
      'Barrio Gotico (Barri Gotic) (419)',
      "La Dreta de l'Eixample (315)",
      'Sant Marti (265)',
      'Sant Pere, Santa Caterina i la Ribera (248)',
      'El Born / La Ribera (222)',
      'El Raval (211)',
      'Gracia (197)',
      "L'Antiga Esquerra de l'Eixample (167)",
      'Vila de Gracia (144)',
      'Ciutadella / Vila Olimpica (138)',
      'Sant Gervasi-Galvany (103)',
      'La Rambla (102)',
      'Les Corts (94)',
      'See all',
      'Good for Couples (503)',
      'Good for a Rainy Day (466)',
      'Budget-friendly (450)',
      'Good for Big Groups (358)',
      'Good for Kids (271)',
      'Free Entry (241)',
      'Hidden Gems (201)',
      'Honeymoon spot (201)',
      'Good for Adrenaline Seekers (129)',
      'Adventurous (54)'],
     'Paris': ['Sights & Landmarks (1,880)',
      'Spas & Wellness (932)',
      'Shopping (842)',
      'Tours (834)',
      'Nightlife (497)',
      'Museums (281)',
      'Transportation (275)',
      'Concerts & Shows (270)',
      'Fun & Games (262)',
      'Food & Drink (251)',
      'Nature & Parks (242)',
      'Outdoor Activities (222)',
      'Classes & Workshops (218)',
      'Day Trips (63)',
      'Traveler Resources (60)',
      'See all',
      'Opera / Bourse (502)',
      '1st Arr. - Louvre (377)',
      '8th Arr. - Elysee (373)',
      '6th Arr. - Luxembourg (345)',
      'Le Marais (341)',
      '16th Arr. - Passy (317)',
      '9th Arr. - Opera (308)',
      '4th Arr. - Hotel-de-Ville (300)',
      '11th Arr. - Popincourt (297)',
      'Louvre / Palais-Royal (281)',
      '5th Arr. - Pantheon (270)',
      'Quartier Latin (267)',
      'Champs-Elysees (260)',
      '7th Arr. - Palais-Bourbon (258)',
      '15th Arr. - Vaugirard (239)',
      'See all',
      'Good for a Rainy Day (717)',
      'Good for Couples (599)',
      'Budget-friendly (433)',
      'Good for Kids (396)',
      'Free Entry (377)',
      'Good for Big Groups (321)',
      'Honeymoon spot (222)',
      'Hidden Gems (221)',
      'Good for Adrenaline Seekers (52)',
      'Adventurous (15)'],
     'Berlin': ['Nightlife (560)',
      'Tours (493)',
      'Sights & Landmarks (477)',
      'Shopping (323)',
      'Spas & Wellness (314)',
      'Museums (257)',
      'Outdoor Activities (198)',
      'Fun & Games (175)',
      'Concerts & Shows (132)',
      'Nature & Parks (81)',
      'Food & Drink (68)',
      'Boat Tours & Water Sports (62)',
      'Classes & Workshops (53)',
      'Traveler Resources (52)',
      'Transportation (29)',
      'See all',
      'Mitte (Borough) (890)',
      'Mitte (637)',
      'Friedrichshain-Kreuzberg (Borough) (386)',
      'Charlottenburg-Wilmersdorf (Borough) (356)',
      'Pankow (Borough) (248)',
      'Charlottenburg (224)',
      'Kreuzberg (219)',
      'Prenzlauer Berg (206)',
      'Friedrichshain (165)',
      'Tempelhof-Schoneberg (Borough) (145)',
      'Tiergarten (135)',
      'Neukolln (Borough) (121)',
      'Neukolln (110)',
      'Schoneberg (94)',
      'Steglitz-Zehlendorf (Borough) (89)',
      'See all',
      'Good for a Rainy Day (380)',
      'Good for Couples (309)',
      'Budget-friendly (283)',
      'Free Entry (255)',
      'Good for Big Groups (239)',
      'Good for Kids (128)',
      'Hidden Gems (111)',
      'Good for Adrenaline Seekers (51)',
      'Honeymoon spot (50)',
      'Adventurous (38)'],
     'Ottawa': ['Sights & Landmarks (96)',
      'Fun & Games (89)',
      'Shopping (77)',
      'Outdoor Activities (76)',
      'Tours (66)',
      'Nightlife (64)',
      'Nature & Parks (59)',
      'Spas & Wellness (56)',
      'Museums (41)',
      'Food & Drink (33)',
      'Concerts & Shows (28)',
      'Boat Tours & Water Sports (21)',
      'Classes & Workshops (12)',
      'Transportation (11)',
      'Traveler Resources (6)',
      'See all',
      'Good for Couples (123)',
      'Good for a Rainy Day (115)',
      'Good for Big Groups (109)',
      'Budget-friendly (104)',
      'Good for Kids (84)',
      'Free Entry (78)',
      'Hidden Gems (28)',
      'Honeymoon spot (19)',
      'Good for Adrenaline Seekers (19)',
      'Adventurous (14)'],
     'Melbourne': ['Tours (388)',
      'Sights & Landmarks (211)',
      'Outdoor Activities (204)',
      'Nightlife (168)',
      'Shopping (163)',
      'Food & Drink (135)',
      'Spas & Wellness (119)',
      'Nature & Parks (112)',
      'Fun & Games (112)',
      'Transportation (97)',
      'Day Trips (71)',
      'Museums (64)',
      'Boat Tours & Water Sports (48)',
      'Concerts & Shows (47)',
      'Classes & Workshops (36)',
      'See all',
      'Central Business District (433)',
      'Chinatown (57)',
      'Southbank (41)',
      'South Melbourne (27)',
      'Docklands (19)',
      'Lygon Street (16)',
      'Chapel Street (15)',
      'Port Melbourne (8)',
      'Parkville (7)',
      'North Melbourne (3)',
      'Fitzroy (3)',
      'Middle Park (1)',
      'Good for Couples (270)',
      'Good for a Rainy Day (270)',
      'Good for Big Groups (266)',
      'Budget-friendly (205)',
      'Free Entry (189)',
      'Good for Kids (132)',
      'Honeymoon spot (66)',
      'Hidden Gems (63)',
      'Adventurous (37)',
      'Good for Adrenaline Seekers (36)'],
     'Zurich': ['Spas & Wellness (143)',
      'Nightlife (110)',
      'Tours (84)',
      'Shopping (83)',
      'Museums (67)',
      'Sights & Landmarks (65)',
      'Outdoor Activities (44)',
      'Transportation (40)',
      'Fun & Games (38)',
      'Nature & Parks (27)',
      'Day Trips (24)',
      'Food & Drink (22)',
      'Classes & Workshops (19)',
      'Concerts & Shows (16)',
      'Boat Tours & Water Sports (13)',
      'See all',
      'Good for a Rainy Day (94)',
      'Free Entry (63)',
      'Good for Couples (57)',
      'Budget-friendly (52)',
      'Good for Big Groups (48)',
      'Good for Kids (44)',
      'Hidden Gems (20)',
      'Honeymoon spot (15)',
      'Good for Adrenaline Seekers (9)',
      'Adventurous (6)'],
     'Oslo': ['Sights & Landmarks (163)',
      'Museums (108)',
      'Shopping (106)',
      'Nightlife (91)',
      'Outdoor Activities (74)',
      'Tours (73)',
      'Fun & Games (67)',
      'Nature & Parks (64)',
      'Spas & Wellness (34)',
      'Concerts & Shows (29)',
      'Boat Tours & Water Sports (21)',
      'Food & Drink (17)',
      'Transportation (11)',
      'Classes & Workshops (11)',
      'Traveler Resources (8)',
      'See all',
      'Good for a Rainy Day (103)',
      'Good for Big Groups (85)',
      'Good for Couples (84)',
      'Budget-friendly (83)',
      'Free Entry (81)',
      'Good for Kids (71)',
      'Hidden Gems (41)',
      'Good for Adrenaline Seekers (21)',
      'Adventurous (16)',
      'Honeymoon spot (16)'],
     'Helsinki': ['Shopping (133)',
      'Sights & Landmarks (119)',
      'Tours (109)',
      'Outdoor Activities (88)',
      'Museums (77)',
      'Nightlife (77)',
      'Fun & Games (66)',
      'Nature & Parks (51)',
      'Spas & Wellness (40)',
      'Boat Tours & Water Sports (30)',
      'Transportation (19)',
      'Concerts & Shows (19)',
      'Food & Drink (12)',
      'Day Trips (9)',
      'Traveler Resources (7)',
      'See all',
      'Good for a Rainy Day (138)',
      'Budget-friendly (102)',
      'Free Entry (96)',
      'Good for Big Groups (83)',
      'Good for Kids (78)',
      'Good for Couples (73)',
      'Hidden Gems (31)',
      'Good for Adrenaline Seekers (21)',
      'Honeymoon spot (17)',
      'Adventurous (15)'],
     'São Paulo': ['Shopping (257)',
      'Sights & Landmarks (246)',
      'Nightlife (246)',
      'Concerts & Shows (233)',
      'Museums (191)',
      'Spas & Wellness (187)',
      'Fun & Games (167)',
      'Tours (140)',
      'Outdoor Activities (107)',
      'Nature & Parks (86)',
      'Transportation (61)',
      'Food & Drink (42)',
      'Traveler Resources (33)',
      'Classes & Workshops (28)',
      'Boat Tours & Water Sports (17)',
      'See all',
      'Jardins (128)',
      'Pinheiros (120)',
      'Bela Vista (96)',
      'Consolacao (60)',
      'Republica (42)',
      'Centro (38)',
      'Vila Mariana (37)',
      'Butanta (29)',
      'Liberdade (25)',
      'Vila Madalena (22)',
      'Vila Buarque (21)',
      'Se (18)',
      'Itaim Bibi (16)',
      'Higienopolis (15)',
      'Ipiranga (14)',
      'See all',
      'Good for a Rainy Day (204)',
      'Good for Kids (182)',
      'Budget-friendly (170)',
      'Free Entry (159)',
      'Good for Big Groups (110)',
      'Good for Couples (95)',
      'Good for Adrenaline Seekers (37)',
      'Hidden Gems (13)',
      'Adventurous (8)',
      'Honeymoon spot (7)'],
     'Hamburg': ['Nightlife (259)',
      'Tours (163)',
      'Sights & Landmarks (148)',
      'Shopping (101)',
      'Museums (79)',
      'Outdoor Activities (74)',
      'Fun & Games (64)',
      'Concerts & Shows (57)',
      'Nature & Parks (48)',
      'Spas & Wellness (36)',
      'Boat Tours & Water Sports (34)',
      'Food & Drink (20)',
      'Classes & Workshops (13)',
      'Transportation (9)',
      'Traveler Resources (4)',
      'See all',
      'Good for a Rainy Day (114)',
      'Free Entry (81)',
      'Good for Big Groups (75)',
      'Budget-friendly (71)',
      'Good for Couples (62)',
      'Good for Kids (49)',
      'Honeymoon spot (23)',
      'Good for Adrenaline Seekers (21)',
      'Hidden Gems (17)',
      'Adventurous (15)'],
     'Milano': ['Sights & Landmarks (684)',
      'Shopping (358)',
      'Nightlife (303)',
      'Tours (212)',
      'Museums (191)',
      'Spas & Wellness (170)',
      'Food & Drink (103)',
      'Fun & Games (90)',
      'Nature & Parks (75)',
      'Transportation (72)',
      'Concerts & Shows (66)',
      'Outdoor Activities (66)',
      'Traveler Resources (59)',
      'Classes & Workshops (41)',
      'Day Trips (27)',
      'See all',
      'Centro Storico (886)',
      'Zone 3 (199)',
      'Zone 8 (137)',
      'Zone 9 (130)',
      'Zone 2 (126)',
      'Zone 6 (125)',
      'Zone 4 (107)',
      'Zone 5 (85)',
      'Ticinese (84)',
      'Zone 7 (64)',
      'Navigli (57)',
      'Porta Garibaldi (56)',
      'Porta Nuova (53)',
      "Quadrilatero della Moda (Quad d'Oro) (49)",
      'Porta Venezia (47)',
      'See all',
      'Good for a Rainy Day (234)',
      'Budget-friendly (179)',
      'Good for Couples (164)',
      'Free Entry (153)',
      'Good for Kids (129)',
      'Good for Big Groups (119)',
      'Hidden Gems (57)',
      'Honeymoon spot (36)',
      'Good for Adrenaline Seekers (16)',
      'Adventurous (11)']}




```python
browser.quit()
```


```python
bb_list
```


```python
dikt3 = {'Munich': ['Sights & Landmarks (226)',
  'Tours (168)',
  'Nightlife (152)',
  'Shopping (105)',
  'Museums (69)',
  'Outdoor Activities (66)',
  'Fun & Games (59)',
  'Spas & Wellness (51)',
  'Food & Drink (41)',
  'Concerts & Shows (37)',
  'Transportation (33)',
  'Nature & Parks (26)',
  'Day Trips (21)',
  'Classes & Workshops (19)',
  'Boat Tours & Water Sports (11)',
  'See all',
  'Good for a Rainy Day (127)',
  'Good for Couples (122)',
  'Budget-friendly (108)',
  'Free Entry (106)',
  'Good for Big Groups (103)',
  'Good for Kids (81)',
  'Honeymoon spot (40)',
  'Good for Adrenaline Seekers (18)',
  'Adventurous (16)',
  'Hidden Gems (16)'],
 'Buenos Aires': ['Sights & Landmarks (470)',
  'Tours (418)',
  'Shopping (277)',
  'Nightlife (226)',
  'Concerts & Shows (175)',
  'Museums (163)',
  'Outdoor Activities (158)',
  'Spas & Wellness (152)',
  'Classes & Workshops (119)',
  'Fun & Games (112)',
  'Transportation (94)',
  'Food & Drink (92)',
  'Nature & Parks (78)',
  'Boat Tours & Water Sports (50)',
  'Traveler Resources (15)',
  'See all',
  'El Centro (Downtown) (547)',
  'Palermo (331)',
  'San Nicolas (199)',
  'Recoleta (170)',
  'Microcentro (160)',
  'Montserrat (138)',
  'Retiro (131)',
  'Theater District (109)',
  'Palermo Soho (98)',
  'Balvanera (84)',
  'San Telmo (78)',
  'Palermo Hollywood (57)',
  'Belgrano (54)',
  'Caballito (53)',
  'Villa Crespo (49)',
  'See all',
  'Good for a Rainy Day (267)',
  'Good for Couples (249)',
  'Budget-friendly (249)',
  'Good for Big Groups (200)',
  'Free Entry (179)',
  'Good for Kids (153)',
  'Honeymoon spot (86)',
  'Good for Adrenaline Seekers (50)',
  'Hidden Gems (32)',
  'Adventurous (15)']}
```
data_ttd =soup.find_all("div", class_="attractions-5attraction-overview-pills-PillShelf__pillShelf--3uaz2")
    #things to do (ttd)
    #for i in scrape_data:
        #print(i)
        #print("/n")
    aa=data_ttd[0]#Types of Things to Do in Cıty
    bb=data_ttd[1]#Things to Do in Cıty by Neighborhood
    #cc=data_ttd[2]#Commonly Searched For in Cıty
    aa_list = []
    for i in aa:
        aa_list.append(i.text)

    bb_list =[] 
    for i in bb:
        bb_list.append(i.text)

    #cc_list =[] 
    #for i in cc:
    #    cc_list.append(i.text)
    print("creating dictionaries for")   
       
    city_name_aa_dict[search_key]=aa_list  
    
    
    city_name_bb_dict[search_key]=bb_list


```python
import pandas as pd
```


```python
city_things_dict2 = pd.DataFrame.from_dict(city_things_dict,orient='index')
```


```python
city_things_dict2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>32</th>
      <th>33</th>
      <th>34</th>
      <th>35</th>
      <th>36</th>
      <th>37</th>
      <th>38</th>
      <th>39</th>
      <th>40</th>
      <th>41</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Singapore</th>
      <td>Shopping (492)</td>
      <td>Spas &amp; Wellness (453)</td>
      <td>Sights &amp; Landmarks (327)</td>
      <td>Tours (276)</td>
      <td>Outdoor Activities (195)</td>
      <td>Fun &amp; Games (190)</td>
      <td>Nightlife (171)</td>
      <td>Museums (126)</td>
      <td>Transportation (124)</td>
      <td>Classes &amp; Workshops (124)</td>
      <td>...</td>
      <td>Good for a Rainy Day (382)</td>
      <td>Free Entry (372)</td>
      <td>Budget-friendly (276)</td>
      <td>Good for Couples (259)</td>
      <td>Good for Big Groups (229)</td>
      <td>Good for Kids (211)</td>
      <td>Hidden Gems (80)</td>
      <td>Honeymoon spot (58)</td>
      <td>Good for Adrenaline Seekers (48)</td>
      <td>Adventurous (30)</td>
    </tr>
    <tr>
      <th>Vancouver</th>
      <td>Spas &amp; Wellness (224)</td>
      <td>Tours (216)</td>
      <td>Outdoor Activities (178)</td>
      <td>Shopping (157)</td>
      <td>Sights &amp; Landmarks (106)</td>
      <td>Nightlife (92)</td>
      <td>Food &amp; Drink (70)</td>
      <td>Boat Tours &amp; Water Sports (67)</td>
      <td>Museums (66)</td>
      <td>Nature &amp; Parks (61)</td>
      <td>...</td>
      <td>Good for Couples (221)</td>
      <td>Good for a Rainy Day (186)</td>
      <td>Budget-friendly (156)</td>
      <td>Good for Big Groups (144)</td>
      <td>Free Entry (125)</td>
      <td>Good for Kids (109)</td>
      <td>Hidden Gems (54)</td>
      <td>Honeymoon spot (53)</td>
      <td>Good for Adrenaline Seekers (46)</td>
      <td>Adventurous (28)</td>
    </tr>
    <tr>
      <th>London</th>
      <td>Nightlife (1,223)</td>
      <td>Tours (1,034)</td>
      <td>Sights &amp; Landmarks (977)</td>
      <td>Shopping (938)</td>
      <td>Spas &amp; Wellness (790)</td>
      <td>Fun &amp; Games (526)</td>
      <td>Concerts &amp; Shows (420)</td>
      <td>Museums (410)</td>
      <td>Transportation (407)</td>
      <td>Outdoor Activities (298)</td>
      <td>...</td>
      <td>Good for a Rainy Day (1,650)</td>
      <td>Good for Couples (1,351)</td>
      <td>Free Entry (1,123)</td>
      <td>Budget-friendly (938)</td>
      <td>Good for Big Groups (921)</td>
      <td>Good for Kids (537)</td>
      <td>Hidden Gems (521)</td>
      <td>Adventurous (175)</td>
      <td>Honeymoon spot (147)</td>
      <td>Good for Adrenaline Seekers (124)</td>
    </tr>
    <tr>
      <th>Toronto</th>
      <td>Spas &amp; Wellness (334)</td>
      <td>Shopping (238)</td>
      <td>Nightlife (207)</td>
      <td>Tours (203)</td>
      <td>Fun &amp; Games (184)</td>
      <td>Sights &amp; Landmarks (181)</td>
      <td>Outdoor Activities (146)</td>
      <td>Nature &amp; Parks (114)</td>
      <td>Museums (110)</td>
      <td>Concerts &amp; Shows (97)</td>
      <td>...</td>
      <td>Good for a Rainy Day (269)</td>
      <td>Good for Couples (269)</td>
      <td>Good for Big Groups (211)</td>
      <td>Budget-friendly (170)</td>
      <td>Free Entry (165)</td>
      <td>Good for Kids (120)</td>
      <td>Hidden Gems (64)</td>
      <td>Honeymoon spot (52)</td>
      <td>Good for Adrenaline Seekers (43)</td>
      <td>Adventurous (33)</td>
    </tr>
    <tr>
      <th>Budapest</th>
      <td>Tours (427)</td>
      <td>Sights &amp; Landmarks (330)</td>
      <td>Nightlife (281)</td>
      <td>Shopping (263)</td>
      <td>Fun &amp; Games (201)</td>
      <td>Outdoor Activities (150)</td>
      <td>Spas &amp; Wellness (141)</td>
      <td>Museums (135)</td>
      <td>Food &amp; Drink (131)</td>
      <td>Transportation (79)</td>
      <td>...</td>
      <td>Good for a Rainy Day (335)</td>
      <td>Good for Couples (330)</td>
      <td>Budget-friendly (313)</td>
      <td>Good for Big Groups (281)</td>
      <td>Free Entry (183)</td>
      <td>Good for Kids (171)</td>
      <td>Hidden Gems (124)</td>
      <td>Honeymoon spot (95)</td>
      <td>Good for Adrenaline Seekers (70)</td>
      <td>Adventurous (47)</td>
    </tr>
    <tr>
      <th>Hong Kong</th>
      <td>Shopping (485)</td>
      <td>Sights &amp; Landmarks (350)</td>
      <td>Tours (251)</td>
      <td>Outdoor Activities (195)</td>
      <td>Nature &amp; Parks (174)</td>
      <td>Spas &amp; Wellness (145)</td>
      <td>Museums (112)</td>
      <td>Fun &amp; Games (100)</td>
      <td>Nightlife (96)</td>
      <td>Food &amp; Drink (91)</td>
      <td>...</td>
      <td>Free Entry (381)</td>
      <td>Budget-friendly (257)</td>
      <td>Good for a Rainy Day (252)</td>
      <td>Good for Couples (234)</td>
      <td>Good for Kids (203)</td>
      <td>Good for Big Groups (134)</td>
      <td>Hidden Gems (57)</td>
      <td>Honeymoon spot (40)</td>
      <td>Good for Adrenaline Seekers (22)</td>
      <td>Adventurous (14)</td>
    </tr>
    <tr>
      <th>Stockholm</th>
      <td>Tours (140)</td>
      <td>Sights &amp; Landmarks (119)</td>
      <td>Outdoor Activities (101)</td>
      <td>Shopping (86)</td>
      <td>Museums (77)</td>
      <td>Fun &amp; Games (64)</td>
      <td>Nature &amp; Parks (60)</td>
      <td>Boat Tours &amp; Water Sports (50)</td>
      <td>Nightlife (40)</td>
      <td>Spas &amp; Wellness (39)</td>
      <td>...</td>
      <td>Good for a Rainy Day (141)</td>
      <td>Budget-friendly (127)</td>
      <td>Good for Couples (114)</td>
      <td>Good for Kids (82)</td>
      <td>Free Entry (80)</td>
      <td>Good for Big Groups (79)</td>
      <td>Hidden Gems (36)</td>
      <td>Honeymoon spot (30)</td>
      <td>Good for Adrenaline Seekers (17)</td>
      <td>Adventurous (16)</td>
    </tr>
    <tr>
      <th>Sydney</th>
      <td>Tours (510)</td>
      <td>Outdoor Activities (336)</td>
      <td>Spas &amp; Wellness (282)</td>
      <td>Nightlife (218)</td>
      <td>Shopping (214)</td>
      <td>Sights &amp; Landmarks (187)</td>
      <td>Boat Tours &amp; Water Sports (152)</td>
      <td>Nature &amp; Parks (143)</td>
      <td>Food &amp; Drink (130)</td>
      <td>Fun &amp; Games (128)</td>
      <td>...</td>
      <td>Good for Big Groups (348)</td>
      <td>Good for Couples (334)</td>
      <td>Good for a Rainy Day (277)</td>
      <td>Budget-friendly (274)</td>
      <td>Free Entry (255)</td>
      <td>Good for Kids (187)</td>
      <td>Honeymoon spot (90)</td>
      <td>Hidden Gems (87)</td>
      <td>Good for Adrenaline Seekers (74)</td>
      <td>Adventurous (64)</td>
    </tr>
    <tr>
      <th>Kuala Lumpur</th>
      <td>Tours (193)</td>
      <td>Shopping (155)</td>
      <td>Spas &amp; Wellness (147)</td>
      <td>Transportation (137)</td>
      <td>Sights &amp; Landmarks (106)</td>
      <td>Outdoor Activities (95)</td>
      <td>Nightlife (93)</td>
      <td>Day Trips (76)</td>
      <td>Fun &amp; Games (65)</td>
      <td>Museums (53)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Barcelona</th>
      <td>Tours (823)</td>
      <td>Nightlife (594)</td>
      <td>Spas &amp; Wellness (560)</td>
      <td>Sights &amp; Landmarks (511)</td>
      <td>Outdoor Activities (443)</td>
      <td>Shopping (426)</td>
      <td>Food &amp; Drink (256)</td>
      <td>Fun &amp; Games (210)</td>
      <td>Museums (165)</td>
      <td>Classes &amp; Workshops (150)</td>
      <td>...</td>
      <td>Good for Couples (503)</td>
      <td>Good for a Rainy Day (466)</td>
      <td>Budget-friendly (450)</td>
      <td>Good for Big Groups (358)</td>
      <td>Good for Kids (271)</td>
      <td>Free Entry (241)</td>
      <td>Hidden Gems (201)</td>
      <td>Honeymoon spot (201)</td>
      <td>Good for Adrenaline Seekers (129)</td>
      <td>Adventurous (54)</td>
    </tr>
    <tr>
      <th>Paris</th>
      <td>Sights &amp; Landmarks (1,880)</td>
      <td>Spas &amp; Wellness (932)</td>
      <td>Shopping (842)</td>
      <td>Tours (834)</td>
      <td>Nightlife (497)</td>
      <td>Museums (281)</td>
      <td>Transportation (275)</td>
      <td>Concerts &amp; Shows (270)</td>
      <td>Fun &amp; Games (262)</td>
      <td>Food &amp; Drink (251)</td>
      <td>...</td>
      <td>Good for a Rainy Day (717)</td>
      <td>Good for Couples (599)</td>
      <td>Budget-friendly (433)</td>
      <td>Good for Kids (396)</td>
      <td>Free Entry (377)</td>
      <td>Good for Big Groups (321)</td>
      <td>Honeymoon spot (222)</td>
      <td>Hidden Gems (221)</td>
      <td>Good for Adrenaline Seekers (52)</td>
      <td>Adventurous (15)</td>
    </tr>
    <tr>
      <th>Berlin</th>
      <td>Nightlife (560)</td>
      <td>Tours (493)</td>
      <td>Sights &amp; Landmarks (477)</td>
      <td>Shopping (323)</td>
      <td>Spas &amp; Wellness (314)</td>
      <td>Museums (257)</td>
      <td>Outdoor Activities (198)</td>
      <td>Fun &amp; Games (175)</td>
      <td>Concerts &amp; Shows (132)</td>
      <td>Nature &amp; Parks (81)</td>
      <td>...</td>
      <td>Good for a Rainy Day (380)</td>
      <td>Good for Couples (309)</td>
      <td>Budget-friendly (283)</td>
      <td>Free Entry (255)</td>
      <td>Good for Big Groups (239)</td>
      <td>Good for Kids (128)</td>
      <td>Hidden Gems (111)</td>
      <td>Good for Adrenaline Seekers (51)</td>
      <td>Honeymoon spot (50)</td>
      <td>Adventurous (38)</td>
    </tr>
    <tr>
      <th>Ottawa</th>
      <td>Sights &amp; Landmarks (96)</td>
      <td>Fun &amp; Games (89)</td>
      <td>Shopping (77)</td>
      <td>Outdoor Activities (76)</td>
      <td>Tours (66)</td>
      <td>Nightlife (64)</td>
      <td>Nature &amp; Parks (59)</td>
      <td>Spas &amp; Wellness (56)</td>
      <td>Museums (41)</td>
      <td>Food &amp; Drink (33)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Melbourne</th>
      <td>Tours (388)</td>
      <td>Sights &amp; Landmarks (211)</td>
      <td>Outdoor Activities (204)</td>
      <td>Nightlife (168)</td>
      <td>Shopping (163)</td>
      <td>Food &amp; Drink (135)</td>
      <td>Spas &amp; Wellness (119)</td>
      <td>Nature &amp; Parks (112)</td>
      <td>Fun &amp; Games (112)</td>
      <td>Transportation (97)</td>
      <td>...</td>
      <td>Free Entry (189)</td>
      <td>Good for Kids (132)</td>
      <td>Honeymoon spot (66)</td>
      <td>Hidden Gems (63)</td>
      <td>Adventurous (37)</td>
      <td>Good for Adrenaline Seekers (36)</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Zurich</th>
      <td>Spas &amp; Wellness (143)</td>
      <td>Nightlife (110)</td>
      <td>Tours (84)</td>
      <td>Shopping (83)</td>
      <td>Museums (67)</td>
      <td>Sights &amp; Landmarks (65)</td>
      <td>Outdoor Activities (44)</td>
      <td>Transportation (40)</td>
      <td>Fun &amp; Games (38)</td>
      <td>Nature &amp; Parks (27)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Oslo</th>
      <td>Sights &amp; Landmarks (163)</td>
      <td>Museums (108)</td>
      <td>Shopping (106)</td>
      <td>Nightlife (91)</td>
      <td>Outdoor Activities (74)</td>
      <td>Tours (73)</td>
      <td>Fun &amp; Games (67)</td>
      <td>Nature &amp; Parks (64)</td>
      <td>Spas &amp; Wellness (34)</td>
      <td>Concerts &amp; Shows (29)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Helsinki</th>
      <td>Shopping (133)</td>
      <td>Sights &amp; Landmarks (119)</td>
      <td>Tours (109)</td>
      <td>Outdoor Activities (88)</td>
      <td>Museums (77)</td>
      <td>Nightlife (77)</td>
      <td>Fun &amp; Games (66)</td>
      <td>Nature &amp; Parks (51)</td>
      <td>Spas &amp; Wellness (40)</td>
      <td>Boat Tours &amp; Water Sports (30)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>São Paulo</th>
      <td>Shopping (257)</td>
      <td>Sights &amp; Landmarks (246)</td>
      <td>Nightlife (246)</td>
      <td>Concerts &amp; Shows (233)</td>
      <td>Museums (191)</td>
      <td>Spas &amp; Wellness (187)</td>
      <td>Fun &amp; Games (167)</td>
      <td>Tours (140)</td>
      <td>Outdoor Activities (107)</td>
      <td>Nature &amp; Parks (86)</td>
      <td>...</td>
      <td>Good for a Rainy Day (204)</td>
      <td>Good for Kids (182)</td>
      <td>Budget-friendly (170)</td>
      <td>Free Entry (159)</td>
      <td>Good for Big Groups (110)</td>
      <td>Good for Couples (95)</td>
      <td>Good for Adrenaline Seekers (37)</td>
      <td>Hidden Gems (13)</td>
      <td>Adventurous (8)</td>
      <td>Honeymoon spot (7)</td>
    </tr>
    <tr>
      <th>Hamburg</th>
      <td>Nightlife (259)</td>
      <td>Tours (163)</td>
      <td>Sights &amp; Landmarks (148)</td>
      <td>Shopping (101)</td>
      <td>Museums (79)</td>
      <td>Outdoor Activities (74)</td>
      <td>Fun &amp; Games (64)</td>
      <td>Concerts &amp; Shows (57)</td>
      <td>Nature &amp; Parks (48)</td>
      <td>Spas &amp; Wellness (36)</td>
      <td>...</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
      <td>None</td>
    </tr>
    <tr>
      <th>Milano</th>
      <td>Sights &amp; Landmarks (684)</td>
      <td>Shopping (358)</td>
      <td>Nightlife (303)</td>
      <td>Tours (212)</td>
      <td>Museums (191)</td>
      <td>Spas &amp; Wellness (170)</td>
      <td>Food &amp; Drink (103)</td>
      <td>Fun &amp; Games (90)</td>
      <td>Nature &amp; Parks (75)</td>
      <td>Transportation (72)</td>
      <td>...</td>
      <td>Good for a Rainy Day (234)</td>
      <td>Budget-friendly (179)</td>
      <td>Good for Couples (164)</td>
      <td>Free Entry (153)</td>
      <td>Good for Kids (129)</td>
      <td>Good for Big Groups (119)</td>
      <td>Hidden Gems (57)</td>
      <td>Honeymoon spot (36)</td>
      <td>Good for Adrenaline Seekers (16)</td>
      <td>Adventurous (11)</td>
    </tr>
  </tbody>
</table>
<p>20 rows × 42 columns</p>
</div>




```python
city_things_dict
```




    {'Singapore': ['Shopping (492)',
      'Spas & Wellness (453)',
      'Sights & Landmarks (327)',
      'Tours (276)',
      'Outdoor Activities (195)',
      'Fun & Games (190)',
      'Nightlife (171)',
      'Museums (126)',
      'Transportation (124)',
      'Classes & Workshops (124)',
      'Nature & Parks (121)',
      'Food & Drink (116)',
      'Boat Tours & Water Sports (74)',
      'Concerts & Shows (44)',
      'Events (21)',
      'See all',
      'Central Area/City Area (1,038)',
      'Downtown Core/Downtown Singapore (288)',
      'Central Business District (194)',
      'Rochor (187)',
      'Orchard (182)',
      'Outram (179)',
      'Orchard Road (177)',
      'Chinatown (133)',
      'Colonial District/Civic District (106)',
      'Marina Bay (105)',
      'Boulevard (103)',
      'Singapore River/Riverside (102)',
      'Bukit Merah (94)',
      'Kallang (91)',
      'City Hall (82)',
      'See all',
      'Good for a Rainy Day (382)',
      'Free Entry (372)',
      'Budget-friendly (276)',
      'Good for Couples (259)',
      'Good for Big Groups (229)',
      'Good for Kids (211)',
      'Hidden Gems (80)',
      'Honeymoon spot (58)',
      'Good for Adrenaline Seekers (48)',
      'Adventurous (30)'],
     'Vancouver': ['Spas & Wellness (224)',
      'Tours (216)',
      'Outdoor Activities (178)',
      'Shopping (157)',
      'Sights & Landmarks (106)',
      'Nightlife (92)',
      'Food & Drink (70)',
      'Boat Tours & Water Sports (67)',
      'Museums (66)',
      'Nature & Parks (61)',
      'Fun & Games (56)',
      'Transportation (52)',
      'Concerts & Shows (51)',
      'Classes & Workshops (24)',
      'Day Trips (19)',
      'See all',
      'Central (457)',
      'Downtown (356)',
      'East Vancouver (145)',
      'False Creek (113)',
      'Fairview (113)',
      'Granville Street (88)',
      'Granville Island & Fairview (77)',
      'West End (76)',
      'Robson Street (74)',
      'Kitsilano (72)',
      'Coal Harbour (70)',
      'Yaletown & False Creek North (69)',
      'Gastown (66)',
      'Granville Island (59)',
      'Yaletown (51)',
      'See all',
      'Good for Couples (221)',
      'Good for a Rainy Day (186)',
      'Budget-friendly (156)',
      'Good for Big Groups (144)',
      'Free Entry (125)',
      'Good for Kids (109)',
      'Hidden Gems (54)',
      'Honeymoon spot (53)',
      'Good for Adrenaline Seekers (46)',
      'Adventurous (28)'],
     'London': ['Nightlife (1,223)',
      'Tours (1,034)',
      'Sights & Landmarks (977)',
      'Shopping (938)',
      'Spas & Wellness (790)',
      'Fun & Games (526)',
      'Concerts & Shows (420)',
      'Museums (410)',
      'Transportation (407)',
      'Outdoor Activities (298)',
      'Food & Drink (296)',
      'Classes & Workshops (293)',
      'Nature & Parks (257)',
      'Boat Tours & Water Sports (93)',
      'Day Trips (65)',
      'See all',
      'Soho (262)',
      'City of London (261)',
      'Mayfair (225)',
      'Covent Garden (211)',
      'Westminster (163)',
      'Trafalgar Square / Embankment (139)',
      'Marylebone (134)',
      'Bloomsbury (121)',
      'Southwark (113)',
      'Notting Hill (106)',
      'Holborn (105)',
      'Shoreditch (98)',
      'Chelsea (94)',
      'Fitzrovia (86)',
      "St. James's (84)",
      'See all',
      'Good for a Rainy Day (1,650)',
      'Good for Couples (1,351)',
      'Free Entry (1,123)',
      'Budget-friendly (938)',
      'Good for Big Groups (921)',
      'Good for Kids (537)',
      'Hidden Gems (521)',
      'Adventurous (175)',
      'Honeymoon spot (147)',
      'Good for Adrenaline Seekers (124)'],
     'Toronto': ['Spas & Wellness (334)',
      'Shopping (238)',
      'Nightlife (207)',
      'Tours (203)',
      'Fun & Games (184)',
      'Sights & Landmarks (181)',
      'Outdoor Activities (146)',
      'Nature & Parks (114)',
      'Museums (110)',
      'Concerts & Shows (97)',
      'Food & Drink (72)',
      'Transportation (70)',
      'Classes & Workshops (58)',
      'Boat Tours & Water Sports (47)',
      'Day Trips (26)',
      'See all',
      'Old Toronto (1,089)',
      'Downtown (639)',
      'Waterfront Communities-The Island (225)',
      'Downtown West (200)',
      'Midtown (167)',
      'West End (130)',
      'Entertainment District (126)',
      'North York (126)',
      'Etobicoke (116)',
      'East End (111)',
      'Church-Yonge Corridor (103)',
      'Bay Street Corridor (98)',
      'Annex (87)',
      'Scarborough (86)',
      'Kensington-Chinatown (66)',
      'See all',
      'Good for a Rainy Day (269)',
      'Good for Couples (269)',
      'Good for Big Groups (211)',
      'Budget-friendly (170)',
      'Free Entry (165)',
      'Good for Kids (120)',
      'Hidden Gems (64)',
      'Honeymoon spot (52)',
      'Good for Adrenaline Seekers (43)',
      'Adventurous (33)'],
     'Budapest': ['Tours (427)',
      'Sights & Landmarks (330)',
      'Nightlife (281)',
      'Shopping (263)',
      'Fun & Games (201)',
      'Outdoor Activities (150)',
      'Spas & Wellness (141)',
      'Museums (135)',
      'Food & Drink (131)',
      'Transportation (79)',
      'Concerts & Shows (61)',
      'Nature & Parks (43)',
      'Classes & Workshops (41)',
      'Boat Tours & Water Sports (37)',
      'Traveler Resources (7)',
      'See all',
      'District V / Inner City (297)',
      'District VII / Jewish Quarter (194)',
      'District I / Buda (147)',
      'Várkerület (33)',
      'Gellert Hill (30)',
      'Belváros-Lipótváros (18)',
      'Terézváros (13)',
      'Margaret Island (8)',
      'Erzsébetváros (7)',
      'Óbuda-Békásmegyer (6)',
      'Zugló (5)',
      'Kispest (5)',
      'Andrássy út (4)',
      'Városliget (4)',
      'Sasad (3)',
      'See all',
      'Good for a Rainy Day (335)',
      'Good for Couples (330)',
      'Budget-friendly (313)',
      'Good for Big Groups (281)',
      'Free Entry (183)',
      'Good for Kids (171)',
      'Hidden Gems (124)',
      'Honeymoon spot (95)',
      'Good for Adrenaline Seekers (70)',
      'Adventurous (47)'],
     'Hong Kong': ['Shopping (485)',
      'Sights & Landmarks (350)',
      'Tours (251)',
      'Outdoor Activities (195)',
      'Nature & Parks (174)',
      'Spas & Wellness (145)',
      'Museums (112)',
      'Fun & Games (100)',
      'Nightlife (96)',
      'Food & Drink (91)',
      'Classes & Workshops (69)',
      'Boat Tours & Water Sports (67)',
      'Transportation (48)',
      'Concerts & Shows (23)',
      'Events (18)',
      'See all',
      'Hong Kong Island (436)',
      'Kowloon (242)',
      'New Territories (232)',
      'Central District (224)',
      'Yau Tsim Mong District (171)',
      'Central (135)',
      'Tsim Sha Tsui (95)',
      'Southern District (50)',
      'Islands District (50)',
      'Sheung Wan (49)',
      'Mong Kok (39)',
      'Eastern District (36)',
      'Sai Kung (35)',
      'Yuen Long (34)',
      'Sha Tin (34)',
      'See all',
      'Free Entry (381)',
      'Budget-friendly (257)',
      'Good for a Rainy Day (252)',
      'Good for Couples (234)',
      'Good for Kids (203)',
      'Good for Big Groups (134)',
      'Hidden Gems (57)',
      'Honeymoon spot (40)',
      'Good for Adrenaline Seekers (22)',
      'Adventurous (14)'],
     'Stockholm': ['Tours (140)',
      'Sights & Landmarks (119)',
      'Outdoor Activities (101)',
      'Shopping (86)',
      'Museums (77)',
      'Fun & Games (64)',
      'Nature & Parks (60)',
      'Boat Tours & Water Sports (50)',
      'Nightlife (40)',
      'Spas & Wellness (39)',
      'Concerts & Shows (28)',
      'Transportation (21)',
      'Food & Drink (21)',
      'Classes & Workshops (10)',
      'Traveler Resources (9)',
      'See all',
      'Norrmalm (120)',
      'Sodermalm Borough (87)',
      'Sodermalm (82)',
      'Gamla Stan & Riddarholmen (80)',
      'Ostermalm (78)',
      'Kungsholmen (32)',
      'Vasastan (32)',
      'Djurgarden & Djurgardsbrunn (32)',
      'SoFo & Medborgarplatsen (25)',
      'Enskede-Arsta-Vantor Borough (20)',
      'Mariatorget (16)',
      'Hornstull & Langholmen (13)',
      'Johanneshov (10)',
      'Slussen (10)',
      'Skeppsholmen (8)',
      'See all',
      'Good for a Rainy Day (141)',
      'Budget-friendly (127)',
      'Good for Couples (114)',
      'Good for Kids (82)',
      'Free Entry (80)',
      'Good for Big Groups (79)',
      'Hidden Gems (36)',
      'Honeymoon spot (30)',
      'Good for Adrenaline Seekers (17)',
      'Adventurous (16)'],
     'Sydney': ['Tours (510)',
      'Outdoor Activities (336)',
      'Spas & Wellness (282)',
      'Nightlife (218)',
      'Shopping (214)',
      'Sights & Landmarks (187)',
      'Boat Tours & Water Sports (152)',
      'Nature & Parks (143)',
      'Food & Drink (130)',
      'Fun & Games (128)',
      'Transportation (110)',
      'Museums (99)',
      'Concerts & Shows (57)',
      'Classes & Workshops (57)',
      'Day Trips (37)',
      'See all',
      'Central Business District (367)',
      'The Rocks (81)',
      'Surry Hills (60)',
      'Darlinghurst (53)',
      'Paddington (46)',
      'Darling Harbour (44)',
      'Newtown (43)',
      'Balmain (30)',
      'Double Bay (26)',
      'Chinatown (21)',
      'Glebe (18)',
      'Inner West (12)',
      'Inner East (11)',
      'Manly (10)',
      'Mosman (10)',
      'See all',
      'Good for Big Groups (348)',
      'Good for Couples (334)',
      'Good for a Rainy Day (277)',
      'Budget-friendly (274)',
      'Free Entry (255)',
      'Good for Kids (187)',
      'Honeymoon spot (90)',
      'Hidden Gems (87)',
      'Good for Adrenaline Seekers (74)',
      'Adventurous (64)'],
     'Kuala Lumpur': ['Tours (193)',
      'Shopping (155)',
      'Spas & Wellness (147)',
      'Transportation (137)',
      'Sights & Landmarks (106)',
      'Outdoor Activities (95)',
      'Nightlife (93)',
      'Day Trips (76)',
      'Fun & Games (65)',
      'Museums (53)',
      'Food & Drink (47)',
      'Classes & Workshops (46)',
      'Nature & Parks (35)',
      'Concerts & Shows (18)',
      'Boat Tours & Water Sports (14)',
      'See all',
      'Good for a Rainy Day (188)',
      'Free Entry (154)',
      'Budget-friendly (150)',
      'Good for Couples (149)',
      'Good for Big Groups (130)',
      'Good for Kids (119)',
      'Hidden Gems (29)',
      'Honeymoon spot (26)',
      'Good for Adrenaline Seekers (24)',
      'Adventurous (14)'],
     'Barcelona': ['Tours (823)',
      'Nightlife (594)',
      'Spas & Wellness (560)',
      'Sights & Landmarks (511)',
      'Outdoor Activities (443)',
      'Shopping (426)',
      'Food & Drink (256)',
      'Fun & Games (210)',
      'Museums (165)',
      'Classes & Workshops (150)',
      'Boat Tours & Water Sports (126)',
      'Transportation (118)',
      'Concerts & Shows (116)',
      'Nature & Parks (115)',
      'Day Trips (63)',
      'See all',
      'Ciutat Vella (Old Town) (956)',
      'Eixample (742)',
      'Barrio Gotico (Barri Gotic) (419)',
      "La Dreta de l'Eixample (315)",
      'Sant Marti (265)',
      'Sant Pere, Santa Caterina i la Ribera (248)',
      'El Born / La Ribera (222)',
      'El Raval (211)',
      'Gracia (197)',
      "L'Antiga Esquerra de l'Eixample (167)",
      'Vila de Gracia (144)',
      'Ciutadella / Vila Olimpica (138)',
      'Sant Gervasi-Galvany (103)',
      'La Rambla (102)',
      'Les Corts (94)',
      'See all',
      'Good for Couples (503)',
      'Good for a Rainy Day (466)',
      'Budget-friendly (450)',
      'Good for Big Groups (358)',
      'Good for Kids (271)',
      'Free Entry (241)',
      'Hidden Gems (201)',
      'Honeymoon spot (201)',
      'Good for Adrenaline Seekers (129)',
      'Adventurous (54)'],
     'Paris': ['Sights & Landmarks (1,880)',
      'Spas & Wellness (932)',
      'Shopping (842)',
      'Tours (834)',
      'Nightlife (497)',
      'Museums (281)',
      'Transportation (275)',
      'Concerts & Shows (270)',
      'Fun & Games (262)',
      'Food & Drink (251)',
      'Nature & Parks (242)',
      'Outdoor Activities (222)',
      'Classes & Workshops (218)',
      'Day Trips (63)',
      'Traveler Resources (60)',
      'See all',
      'Opera / Bourse (502)',
      '1st Arr. - Louvre (377)',
      '8th Arr. - Elysee (373)',
      '6th Arr. - Luxembourg (345)',
      'Le Marais (341)',
      '16th Arr. - Passy (317)',
      '9th Arr. - Opera (308)',
      '4th Arr. - Hotel-de-Ville (300)',
      '11th Arr. - Popincourt (297)',
      'Louvre / Palais-Royal (281)',
      '5th Arr. - Pantheon (270)',
      'Quartier Latin (267)',
      'Champs-Elysees (260)',
      '7th Arr. - Palais-Bourbon (258)',
      '15th Arr. - Vaugirard (239)',
      'See all',
      'Good for a Rainy Day (717)',
      'Good for Couples (599)',
      'Budget-friendly (433)',
      'Good for Kids (396)',
      'Free Entry (377)',
      'Good for Big Groups (321)',
      'Honeymoon spot (222)',
      'Hidden Gems (221)',
      'Good for Adrenaline Seekers (52)',
      'Adventurous (15)'],
     'Berlin': ['Nightlife (560)',
      'Tours (493)',
      'Sights & Landmarks (477)',
      'Shopping (323)',
      'Spas & Wellness (314)',
      'Museums (257)',
      'Outdoor Activities (198)',
      'Fun & Games (175)',
      'Concerts & Shows (132)',
      'Nature & Parks (81)',
      'Food & Drink (68)',
      'Boat Tours & Water Sports (62)',
      'Classes & Workshops (53)',
      'Traveler Resources (52)',
      'Transportation (29)',
      'See all',
      'Mitte (Borough) (890)',
      'Mitte (637)',
      'Friedrichshain-Kreuzberg (Borough) (386)',
      'Charlottenburg-Wilmersdorf (Borough) (356)',
      'Pankow (Borough) (248)',
      'Charlottenburg (224)',
      'Kreuzberg (219)',
      'Prenzlauer Berg (206)',
      'Friedrichshain (165)',
      'Tempelhof-Schoneberg (Borough) (145)',
      'Tiergarten (135)',
      'Neukolln (Borough) (121)',
      'Neukolln (110)',
      'Schoneberg (94)',
      'Steglitz-Zehlendorf (Borough) (89)',
      'See all',
      'Good for a Rainy Day (380)',
      'Good for Couples (309)',
      'Budget-friendly (283)',
      'Free Entry (255)',
      'Good for Big Groups (239)',
      'Good for Kids (128)',
      'Hidden Gems (111)',
      'Good for Adrenaline Seekers (51)',
      'Honeymoon spot (50)',
      'Adventurous (38)'],
     'Ottawa': ['Sights & Landmarks (96)',
      'Fun & Games (89)',
      'Shopping (77)',
      'Outdoor Activities (76)',
      'Tours (66)',
      'Nightlife (64)',
      'Nature & Parks (59)',
      'Spas & Wellness (56)',
      'Museums (41)',
      'Food & Drink (33)',
      'Concerts & Shows (28)',
      'Boat Tours & Water Sports (21)',
      'Classes & Workshops (12)',
      'Transportation (11)',
      'Traveler Resources (6)',
      'See all',
      'Good for Couples (123)',
      'Good for a Rainy Day (115)',
      'Good for Big Groups (109)',
      'Budget-friendly (104)',
      'Good for Kids (84)',
      'Free Entry (78)',
      'Hidden Gems (28)',
      'Honeymoon spot (19)',
      'Good for Adrenaline Seekers (19)',
      'Adventurous (14)'],
     'Melbourne': ['Tours (388)',
      'Sights & Landmarks (211)',
      'Outdoor Activities (204)',
      'Nightlife (168)',
      'Shopping (163)',
      'Food & Drink (135)',
      'Spas & Wellness (119)',
      'Nature & Parks (112)',
      'Fun & Games (112)',
      'Transportation (97)',
      'Day Trips (71)',
      'Museums (64)',
      'Boat Tours & Water Sports (48)',
      'Concerts & Shows (47)',
      'Classes & Workshops (36)',
      'See all',
      'Central Business District (433)',
      'Chinatown (57)',
      'Southbank (41)',
      'South Melbourne (27)',
      'Docklands (19)',
      'Lygon Street (16)',
      'Chapel Street (15)',
      'Port Melbourne (8)',
      'Parkville (7)',
      'North Melbourne (3)',
      'Fitzroy (3)',
      'Middle Park (1)',
      'Good for Couples (270)',
      'Good for a Rainy Day (270)',
      'Good for Big Groups (266)',
      'Budget-friendly (205)',
      'Free Entry (189)',
      'Good for Kids (132)',
      'Honeymoon spot (66)',
      'Hidden Gems (63)',
      'Adventurous (37)',
      'Good for Adrenaline Seekers (36)'],
     'Zurich': ['Spas & Wellness (143)',
      'Nightlife (110)',
      'Tours (84)',
      'Shopping (83)',
      'Museums (67)',
      'Sights & Landmarks (65)',
      'Outdoor Activities (44)',
      'Transportation (40)',
      'Fun & Games (38)',
      'Nature & Parks (27)',
      'Day Trips (24)',
      'Food & Drink (22)',
      'Classes & Workshops (19)',
      'Concerts & Shows (16)',
      'Boat Tours & Water Sports (13)',
      'See all',
      'Good for a Rainy Day (94)',
      'Free Entry (63)',
      'Good for Couples (57)',
      'Budget-friendly (52)',
      'Good for Big Groups (48)',
      'Good for Kids (44)',
      'Hidden Gems (20)',
      'Honeymoon spot (15)',
      'Good for Adrenaline Seekers (9)',
      'Adventurous (6)'],
     'Oslo': ['Sights & Landmarks (163)',
      'Museums (108)',
      'Shopping (106)',
      'Nightlife (91)',
      'Outdoor Activities (74)',
      'Tours (73)',
      'Fun & Games (67)',
      'Nature & Parks (64)',
      'Spas & Wellness (34)',
      'Concerts & Shows (29)',
      'Boat Tours & Water Sports (21)',
      'Food & Drink (17)',
      'Transportation (11)',
      'Classes & Workshops (11)',
      'Traveler Resources (8)',
      'See all',
      'Good for a Rainy Day (103)',
      'Good for Big Groups (85)',
      'Good for Couples (84)',
      'Budget-friendly (83)',
      'Free Entry (81)',
      'Good for Kids (71)',
      'Hidden Gems (41)',
      'Good for Adrenaline Seekers (21)',
      'Adventurous (16)',
      'Honeymoon spot (16)'],
     'Helsinki': ['Shopping (133)',
      'Sights & Landmarks (119)',
      'Tours (109)',
      'Outdoor Activities (88)',
      'Museums (77)',
      'Nightlife (77)',
      'Fun & Games (66)',
      'Nature & Parks (51)',
      'Spas & Wellness (40)',
      'Boat Tours & Water Sports (30)',
      'Transportation (19)',
      'Concerts & Shows (19)',
      'Food & Drink (12)',
      'Day Trips (9)',
      'Traveler Resources (7)',
      'See all',
      'Good for a Rainy Day (138)',
      'Budget-friendly (102)',
      'Free Entry (96)',
      'Good for Big Groups (83)',
      'Good for Kids (78)',
      'Good for Couples (73)',
      'Hidden Gems (31)',
      'Good for Adrenaline Seekers (21)',
      'Honeymoon spot (17)',
      'Adventurous (15)'],
     'São Paulo': ['Shopping (257)',
      'Sights & Landmarks (246)',
      'Nightlife (246)',
      'Concerts & Shows (233)',
      'Museums (191)',
      'Spas & Wellness (187)',
      'Fun & Games (167)',
      'Tours (140)',
      'Outdoor Activities (107)',
      'Nature & Parks (86)',
      'Transportation (61)',
      'Food & Drink (42)',
      'Traveler Resources (33)',
      'Classes & Workshops (28)',
      'Boat Tours & Water Sports (17)',
      'See all',
      'Jardins (128)',
      'Pinheiros (120)',
      'Bela Vista (96)',
      'Consolacao (60)',
      'Republica (42)',
      'Centro (38)',
      'Vila Mariana (37)',
      'Butanta (29)',
      'Liberdade (25)',
      'Vila Madalena (22)',
      'Vila Buarque (21)',
      'Se (18)',
      'Itaim Bibi (16)',
      'Higienopolis (15)',
      'Ipiranga (14)',
      'See all',
      'Good for a Rainy Day (204)',
      'Good for Kids (182)',
      'Budget-friendly (170)',
      'Free Entry (159)',
      'Good for Big Groups (110)',
      'Good for Couples (95)',
      'Good for Adrenaline Seekers (37)',
      'Hidden Gems (13)',
      'Adventurous (8)',
      'Honeymoon spot (7)'],
     'Hamburg': ['Nightlife (259)',
      'Tours (163)',
      'Sights & Landmarks (148)',
      'Shopping (101)',
      'Museums (79)',
      'Outdoor Activities (74)',
      'Fun & Games (64)',
      'Concerts & Shows (57)',
      'Nature & Parks (48)',
      'Spas & Wellness (36)',
      'Boat Tours & Water Sports (34)',
      'Food & Drink (20)',
      'Classes & Workshops (13)',
      'Transportation (9)',
      'Traveler Resources (4)',
      'See all',
      'Good for a Rainy Day (114)',
      'Free Entry (81)',
      'Good for Big Groups (75)',
      'Budget-friendly (71)',
      'Good for Couples (62)',
      'Good for Kids (49)',
      'Honeymoon spot (23)',
      'Good for Adrenaline Seekers (21)',
      'Hidden Gems (17)',
      'Adventurous (15)'],
     'Milano': ['Sights & Landmarks (684)',
      'Shopping (358)',
      'Nightlife (303)',
      'Tours (212)',
      'Museums (191)',
      'Spas & Wellness (170)',
      'Food & Drink (103)',
      'Fun & Games (90)',
      'Nature & Parks (75)',
      'Transportation (72)',
      'Concerts & Shows (66)',
      'Outdoor Activities (66)',
      'Traveler Resources (59)',
      'Classes & Workshops (41)',
      'Day Trips (27)',
      'See all',
      'Centro Storico (886)',
      'Zone 3 (199)',
      'Zone 8 (137)',
      'Zone 9 (130)',
      'Zone 2 (126)',
      'Zone 6 (125)',
      'Zone 4 (107)',
      'Zone 5 (85)',
      'Ticinese (84)',
      'Zone 7 (64)',
      'Navigli (57)',
      'Porta Garibaldi (56)',
      'Porta Nuova (53)',
      "Quadrilatero della Moda (Quad d'Oro) (49)",
      'Porta Venezia (47)',
      'See all',
      'Good for a Rainy Day (234)',
      'Budget-friendly (179)',
      'Good for Couples (164)',
      'Free Entry (153)',
      'Good for Kids (129)',
      'Good for Big Groups (119)',
      'Hidden Gems (57)',
      'Honeymoon spot (36)',
      'Good for Adrenaline Seekers (16)',
      'Adventurous (11)']}




```python
dikt3={'Singapore': ['Shopping (492)',
  'Spas & Wellness (453)',
  'Sights & Landmarks (327)',
  'Tours (276)',
  'Outdoor Activities (195)',
  'Fun & Games (190)',
  'Nightlife (171)',
  'Museums (126)',
  'Transportation (124)',
  'Classes & Workshops (124)',
  'Nature & Parks (121)',
  'Food & Drink (116)',
  'Boat Tours & Water Sports (74)',
  'Concerts & Shows (44)',
  'Events (21)',
  'See all',
  'Central Area/City Area (1,038)',
  'Downtown Core/Downtown Singapore (288)',
  'Central Business District (194)',
  'Rochor (187)',
  'Orchard (182)',
  'Outram (179)',
  'Orchard Road (177)',
  'Chinatown (133)',
  'Colonial District/Civic District (106)',
  'Marina Bay (105)',
  'Boulevard (103)',
  'Singapore River/Riverside (102)',
  'Bukit Merah (94)',
  'Kallang (91)',
  'City Hall (82)',
  'See all',
  'Good for a Rainy Day (382)',
  'Free Entry (372)',
  'Budget-friendly (276)',
  'Good for Couples (259)',
  'Good for Big Groups (229)',
  'Good for Kids (211)',
  'Hidden Gems (80)',
  'Honeymoon spot (58)',
  'Good for Adrenaline Seekers (48)',
  'Adventurous (30)'],
 'Vancouver': ['Spas & Wellness (224)',
  'Tours (216)',
  'Outdoor Activities (178)',
  'Shopping (157)',
  'Sights & Landmarks (106)',
  'Nightlife (92)',
  'Food & Drink (70)',
  'Boat Tours & Water Sports (67)',
  'Museums (66)',
  'Nature & Parks (61)',
  'Fun & Games (56)',
  'Transportation (52)',
  'Concerts & Shows (51)',
  'Classes & Workshops (24)',
  'Day Trips (19)',
  'See all',
  'Central (457)',
  'Downtown (356)',
  'East Vancouver (145)',
  'False Creek (113)',
  'Fairview (113)',
  'Granville Street (88)',
  'Granville Island & Fairview (77)',
  'West End (76)',
  'Robson Street (74)',
  'Kitsilano (72)',
  'Coal Harbour (70)',
  'Yaletown & False Creek North (69)',
  'Gastown (66)',
  'Granville Island (59)',
  'Yaletown (51)',
  'See all',
  'Good for Couples (221)',
  'Good for a Rainy Day (186)',
  'Budget-friendly (156)',
  'Good for Big Groups (144)',
  'Free Entry (125)',
  'Good for Kids (109)',
  'Hidden Gems (54)',
  'Honeymoon spot (53)',
  'Good for Adrenaline Seekers (46)',
  'Adventurous (28)'],
 'London': ['Nightlife (1,223)',
  'Tours (1,034)',
  'Sights & Landmarks (977)',
  'Shopping (938)',
  'Spas & Wellness (790)',
  'Fun & Games (526)',
  'Concerts & Shows (420)',
  'Museums (410)',
  'Transportation (407)',
  'Outdoor Activities (298)',
  'Food & Drink (296)',
  'Classes & Workshops (293)',
  'Nature & Parks (257)',
  'Boat Tours & Water Sports (93)',
  'Day Trips (65)',
  'See all',
  'Soho (262)',
  'City of London (261)',
  'Mayfair (225)',
  'Covent Garden (211)',
  'Westminster (163)',
  'Trafalgar Square / Embankment (139)',
  'Marylebone (134)',
  'Bloomsbury (121)',
  'Southwark (113)',
  'Notting Hill (106)',
  'Holborn (105)',
  'Shoreditch (98)',
  'Chelsea (94)',
  'Fitzrovia (86)',
  "St. James's (84)",
  'See all',
  'Good for a Rainy Day (1,650)',
  'Good for Couples (1,351)',
  'Free Entry (1,123)',
  'Budget-friendly (938)',
  'Good for Big Groups (921)',
  'Good for Kids (537)',
  'Hidden Gems (521)',
  'Adventurous (175)',
  'Honeymoon spot (147)',
  'Good for Adrenaline Seekers (124)'],
 'Toronto': ['Spas & Wellness (334)',
  'Shopping (238)',
  'Nightlife (207)',
  'Tours (203)',
  'Fun & Games (184)',
  'Sights & Landmarks (181)',
  'Outdoor Activities (146)',
  'Nature & Parks (114)',
  'Museums (110)',
  'Concerts & Shows (97)',
  'Food & Drink (72)',
  'Transportation (70)',
  'Classes & Workshops (58)',
  'Boat Tours & Water Sports (47)',
  'Day Trips (26)',
  'See all',
  'Old Toronto (1,089)',
  'Downtown (639)',
  'Waterfront Communities-The Island (225)',
  'Downtown West (200)',
  'Midtown (167)',
  'West End (130)',
  'Entertainment District (126)',
  'North York (126)',
  'Etobicoke (116)',
  'East End (111)',
  'Church-Yonge Corridor (103)',
  'Bay Street Corridor (98)',
  'Annex (87)',
  'Scarborough (86)',
  'Kensington-Chinatown (66)',
  'See all',
  'Good for a Rainy Day (269)',
  'Good for Couples (269)',
  'Good for Big Groups (211)',
  'Budget-friendly (170)',
  'Free Entry (165)',
  'Good for Kids (120)',
  'Hidden Gems (64)',
  'Honeymoon spot (52)',
  'Good for Adrenaline Seekers (43)',
  'Adventurous (33)'],
 'Budapest': ['Tours (427)',
  'Sights & Landmarks (330)',
  'Nightlife (281)',
  'Shopping (263)',
  'Fun & Games (201)',
  'Outdoor Activities (150)',
  'Spas & Wellness (141)',
  'Museums (135)',
  'Food & Drink (131)',
  'Transportation (79)',
  'Concerts & Shows (61)',
  'Nature & Parks (43)',
  'Classes & Workshops (41)',
  'Boat Tours & Water Sports (37)',
  'Traveler Resources (7)',
  'See all',
  'District V / Inner City (297)',
  'District VII / Jewish Quarter (194)',
  'District I / Buda (147)',
  'Várkerület (33)',
  'Gellert Hill (30)',
  'Belváros-Lipótváros (18)',
  'Terézváros (13)',
  'Margaret Island (8)',
  'Erzsébetváros (7)',
  'Óbuda-Békásmegyer (6)',
  'Zugló (5)',
  'Kispest (5)',
  'Andrássy út (4)',
  'Városliget (4)',
  'Sasad (3)',
  'See all',
  'Good for a Rainy Day (335)',
  'Good for Couples (330)',
  'Budget-friendly (313)',
  'Good for Big Groups (281)',
  'Free Entry (183)',
  'Good for Kids (171)',
  'Hidden Gems (124)',
  'Honeymoon spot (95)',
  'Good for Adrenaline Seekers (70)',
  'Adventurous (47)'],
 'Hong Kong': ['Shopping (485)',
  'Sights & Landmarks (350)',
  'Tours (251)',
  'Outdoor Activities (195)',
  'Nature & Parks (174)',
  'Spas & Wellness (145)',
  'Museums (112)',
  'Fun & Games (100)',
  'Nightlife (96)',
  'Food & Drink (91)',
  'Classes & Workshops (69)',
  'Boat Tours & Water Sports (67)',
  'Transportation (48)',
  'Concerts & Shows (23)',
  'Events (18)',
  'See all',
  'Hong Kong Island (436)',
  'Kowloon (242)',
  'New Territories (232)',
  'Central District (224)',
  'Yau Tsim Mong District (171)',
  'Central (135)',
  'Tsim Sha Tsui (95)',
  'Southern District (50)',
  'Islands District (50)',
  'Sheung Wan (49)',
  'Mong Kok (39)',
  'Eastern District (36)',
  'Sai Kung (35)',
  'Yuen Long (34)',
  'Sha Tin (34)',
  'See all',
  'Free Entry (381)',
  'Budget-friendly (257)',
  'Good for a Rainy Day (252)',
  'Good for Couples (234)',
  'Good for Kids (203)',
  'Good for Big Groups (134)',
  'Hidden Gems (57)',
  'Honeymoon spot (40)',
  'Good for Adrenaline Seekers (22)',
  'Adventurous (14)'],
 'Stockholm': ['Tours (140)',
  'Sights & Landmarks (119)',
  'Outdoor Activities (101)',
  'Shopping (86)',
  'Museums (77)',
  'Fun & Games (64)',
  'Nature & Parks (60)',
  'Boat Tours & Water Sports (50)',
  'Nightlife (40)',
  'Spas & Wellness (39)',
  'Concerts & Shows (28)',
  'Transportation (21)',
  'Food & Drink (21)',
  'Classes & Workshops (10)',
  'Traveler Resources (9)',
  'See all',
  'Norrmalm (120)',
  'Sodermalm Borough (87)',
  'Sodermalm (82)',
  'Gamla Stan & Riddarholmen (80)',
  'Ostermalm (78)',
  'Kungsholmen (32)',
  'Vasastan (32)',
  'Djurgarden & Djurgardsbrunn (32)',
  'SoFo & Medborgarplatsen (25)',
  'Enskede-Arsta-Vantor Borough (20)',
  'Mariatorget (16)',
  'Hornstull & Langholmen (13)',
  'Johanneshov (10)',
  'Slussen (10)',
  'Skeppsholmen (8)',
  'See all',
  'Good for a Rainy Day (141)',
  'Budget-friendly (127)',
  'Good for Couples (114)',
  'Good for Kids (82)',
  'Free Entry (80)',
  'Good for Big Groups (79)',
  'Hidden Gems (36)',
  'Honeymoon spot (30)',
  'Good for Adrenaline Seekers (17)',
  'Adventurous (16)'],
 'Sydney': ['Tours (510)',
  'Outdoor Activities (336)',
  'Spas & Wellness (282)',
  'Nightlife (218)',
  'Shopping (214)',
  'Sights & Landmarks (187)',
  'Boat Tours & Water Sports (152)',
  'Nature & Parks (143)',
  'Food & Drink (130)',
  'Fun & Games (128)',
  'Transportation (110)',
  'Museums (99)',
  'Concerts & Shows (57)',
  'Classes & Workshops (57)',
  'Day Trips (37)',
  'See all',
  'Central Business District (367)',
  'The Rocks (81)',
  'Surry Hills (60)',
  'Darlinghurst (53)',
  'Paddington (46)',
  'Darling Harbour (44)',
  'Newtown (43)',
  'Balmain (30)',
  'Double Bay (26)',
  'Chinatown (21)',
  'Glebe (18)',
  'Inner West (12)',
  'Inner East (11)',
  'Manly (10)',
  'Mosman (10)',
  'See all',
  'Good for Big Groups (348)',
  'Good for Couples (334)',
  'Good for a Rainy Day (277)',
  'Budget-friendly (274)',
  'Free Entry (255)',
  'Good for Kids (187)',
  'Honeymoon spot (90)',
  'Hidden Gems (87)',
  'Good for Adrenaline Seekers (74)',
  'Adventurous (64)'],
 'Kuala Lumpur': ['Tours (193)',
  'Shopping (155)',
  'Spas & Wellness (147)',
  'Transportation (137)',
  'Sights & Landmarks (106)',
  'Outdoor Activities (95)',
  'Nightlife (93)',
  'Day Trips (76)',
  'Fun & Games (65)',
  'Museums (53)',
  'Food & Drink (47)',
  'Classes & Workshops (46)',
  'Nature & Parks (35)',
  'Concerts & Shows (18)',
  'Boat Tours & Water Sports (14)',
  'See all',
  'Good for a Rainy Day (188)',
  'Free Entry (154)',
  'Budget-friendly (150)',
  'Good for Couples (149)',
  'Good for Big Groups (130)',
  'Good for Kids (119)',
  'Hidden Gems (29)',
  'Honeymoon spot (26)',
  'Good for Adrenaline Seekers (24)',
  'Adventurous (14)'],
 'Barcelona': ['Tours (823)',
  'Nightlife (594)',
  'Spas & Wellness (560)',
  'Sights & Landmarks (511)',
  'Outdoor Activities (443)',
  'Shopping (426)',
  'Food & Drink (256)',
  'Fun & Games (210)',
  'Museums (165)',
  'Classes & Workshops (150)',
  'Boat Tours & Water Sports (126)',
  'Transportation (118)',
  'Concerts & Shows (116)',
  'Nature & Parks (115)',
  'Day Trips (63)',
  'See all',
  'Ciutat Vella (Old Town) (956)',
  'Eixample (742)',
  'Barrio Gotico (Barri Gotic) (419)',
  "La Dreta de l'Eixample (315)",
  'Sant Marti (265)',
  'Sant Pere, Santa Caterina i la Ribera (248)',
  'El Born / La Ribera (222)',
  'El Raval (211)',
  'Gracia (197)',
  "L'Antiga Esquerra de l'Eixample (167)",
  'Vila de Gracia (144)',
  'Ciutadella / Vila Olimpica (138)',
  'Sant Gervasi-Galvany (103)',
  'La Rambla (102)',
  'Les Corts (94)',
  'See all',
  'Good for Couples (503)',
  'Good for a Rainy Day (466)',
  'Budget-friendly (450)',
  'Good for Big Groups (358)',
  'Good for Kids (271)',
  'Free Entry (241)',
  'Hidden Gems (201)',
  'Honeymoon spot (201)',
  'Good for Adrenaline Seekers (129)',
  'Adventurous (54)'],
 'Paris': ['Sights & Landmarks (1,880)',
  'Spas & Wellness (932)',
  'Shopping (842)',
  'Tours (834)',
  'Nightlife (497)',
  'Museums (281)',
  'Transportation (275)',
  'Concerts & Shows (270)',
  'Fun & Games (262)',
  'Food & Drink (251)',
  'Nature & Parks (242)',
  'Outdoor Activities (222)',
  'Classes & Workshops (218)',
  'Day Trips (63)',
  'Traveler Resources (60)',
  'See all',
  'Opera / Bourse (502)',
  '1st Arr. - Louvre (377)',
  '8th Arr. - Elysee (373)',
  '6th Arr. - Luxembourg (345)',
  'Le Marais (341)',
  '16th Arr. - Passy (317)',
  '9th Arr. - Opera (308)',
  '4th Arr. - Hotel-de-Ville (300)',
  '11th Arr. - Popincourt (297)',
  'Louvre / Palais-Royal (281)',
  '5th Arr. - Pantheon (270)',
  'Quartier Latin (267)',
  'Champs-Elysees (260)',
  '7th Arr. - Palais-Bourbon (258)',
  '15th Arr. - Vaugirard (239)',
  'See all',
  'Good for a Rainy Day (717)',
  'Good for Couples (599)',
  'Budget-friendly (433)',
  'Good for Kids (396)',
  'Free Entry (377)',
  'Good for Big Groups (321)',
  'Honeymoon spot (222)',
  'Hidden Gems (221)',
  'Good for Adrenaline Seekers (52)',
  'Adventurous (15)'], 'Berlin': ['Nightlife (560)',
  'Tours (493)',
  'Sights & Landmarks (477)',
  'Shopping (323)',
  'Spas & Wellness (314)',
  'Museums (257)',
  'Outdoor Activities (198)',
  'Fun & Games (175)',
  'Concerts & Shows (132)',
  'Nature & Parks (81)',
  'Food & Drink (68)',
  'Boat Tours & Water Sports (62)',
  'Classes & Workshops (53)',
  'Traveler Resources (52)',
  'Transportation (29)',
  'See all',
  'Mitte (Borough) (890)',
  'Mitte (637)',
  'Friedrichshain-Kreuzberg (Borough) (386)',
  'Charlottenburg-Wilmersdorf (Borough) (356)',
  'Pankow (Borough) (248)',
  'Charlottenburg (224)',
  'Kreuzberg (219)',
  'Prenzlauer Berg (206)',
  'Friedrichshain (165)',
  'Tempelhof-Schoneberg (Borough) (145)',
  'Tiergarten (135)',
  'Neukolln (Borough) (121)',
  'Neukolln (110)',
  'Schoneberg (94)',
  'Steglitz-Zehlendorf (Borough) (89)',
  'See all',
  'Good for a Rainy Day (380)',
  'Good for Couples (309)',
  'Budget-friendly (283)',
  'Free Entry (255)',
  'Good for Big Groups (239)',
  'Good for Kids (128)',
  'Hidden Gems (111)',
  'Good for Adrenaline Seekers (51)',
  'Honeymoon spot (50)',
  'Adventurous (38)'],
 'Ottawa': ['Sights & Landmarks (96)',
  'Fun & Games (89)',
  'Shopping (77)',
  'Outdoor Activities (76)',
  'Tours (66)',
  'Nightlife (64)',
  'Nature & Parks (59)',
  'Spas & Wellness (56)',
  'Museums (41)',
  'Food & Drink (33)',
  'Concerts & Shows (28)',
  'Boat Tours & Water Sports (21)',
  'Classes & Workshops (12)',
  'Transportation (11)',
  'Traveler Resources (6)',
  'See all',
  'Good for Couples (123)',
  'Good for a Rainy Day (115)',
  'Good for Big Groups (109)',
  'Budget-friendly (104)',
  'Good for Kids (84)',
  'Free Entry (78)',
  'Hidden Gems (28)',
  'Honeymoon spot (19)',
  'Good for Adrenaline Seekers (19)',
  'Adventurous (14)'],
 'Melbourne': ['Tours (388)',
  'Sights & Landmarks (211)',
  'Outdoor Activities (204)',
  'Nightlife (168)',
  'Shopping (163)',
  'Food & Drink (135)',
  'Spas & Wellness (119)',
  'Nature & Parks (112)',
  'Fun & Games (112)',
  'Transportation (97)',
  'Day Trips (71)',
  'Museums (64)',
  'Boat Tours & Water Sports (48)',
  'Concerts & Shows (47)',
  'Classes & Workshops (36)',
  'See all',
  'Central Business District (433)',
  'Chinatown (57)',
  'Southbank (41)',
  'South Melbourne (27)',
  'Docklands (19)',
  'Lygon Street (16)',
  'Chapel Street (15)',
  'Port Melbourne (8)',
  'Parkville (7)',
  'North Melbourne (3)',
  'Fitzroy (3)',
  'Middle Park (1)',
  'Good for Couples (270)',
  'Good for a Rainy Day (270)',
  'Good for Big Groups (266)',
  'Budget-friendly (205)',
  'Free Entry (189)',
  'Good for Kids (132)',
  'Honeymoon spot (66)',
  'Hidden Gems (63)',
  'Adventurous (37)',
  'Good for Adrenaline Seekers (36)'],
 'Zurich': ['Spas & Wellness (143)',
  'Nightlife (110)',
  'Tours (84)',
  'Shopping (83)',
  'Museums (67)',
  'Sights & Landmarks (65)',
  'Outdoor Activities (44)',
  'Transportation (40)',
  'Fun & Games (38)',
  'Nature & Parks (27)',
  'Day Trips (24)',
  'Food & Drink (22)',
  'Classes & Workshops (19)',
  'Concerts & Shows (16)',
  'Boat Tours & Water Sports (13)',
  'See all',
  'Good for a Rainy Day (94)',
  'Free Entry (63)',
  'Good for Couples (57)',
  'Budget-friendly (52)',
  'Good for Big Groups (48)',
  'Good for Kids (44)',
  'Hidden Gems (20)',
  'Honeymoon spot (15)',
  'Good for Adrenaline Seekers (9)',
  'Adventurous (6)'],
 'Oslo': ['Sights & Landmarks (163)',
  'Museums (108)',
  'Shopping (106)',
  'Nightlife (91)',
  'Outdoor Activities (74)',
  'Tours (73)',
  'Fun & Games (67)',
  'Nature & Parks (64)',
  'Spas & Wellness (34)',
  'Concerts & Shows (29)',
  'Boat Tours & Water Sports (21)',
  'Food & Drink (17)',
  'Transportation (11)',
  'Classes & Workshops (11)',
  'Traveler Resources (8)',
  'See all',
  'Good for a Rainy Day (103)',
  'Good for Big Groups (85)',
  'Good for Couples (84)',
  'Budget-friendly (83)',
  'Free Entry (81)',
  'Good for Kids (71)',
  'Hidden Gems (41)',
  'Good for Adrenaline Seekers (21)',
  'Adventurous (16)',
  'Honeymoon spot (16)'],
 'Helsinki': ['Shopping (133)',
  'Sights & Landmarks (119)',
  'Tours (109)',
  'Outdoor Activities (88)',
  'Museums (77)',
  'Nightlife (77)',
  'Fun & Games (66)',
  'Nature & Parks (51)',
  'Spas & Wellness (40)',
  'Boat Tours & Water Sports (30)',
  'Transportation (19)',
  'Concerts & Shows (19)',
  'Food & Drink (12)',
  'Day Trips (9)',
  'Traveler Resources (7)',
  'See all',
  'Good for a Rainy Day (138)',
  'Budget-friendly (102)',
  'Free Entry (96)',
  'Good for Big Groups (83)',
  'Good for Kids (78)',
  'Good for Couples (73)',
  'Hidden Gems (31)',
  'Good for Adrenaline Seekers (21)',
  'Honeymoon spot (17)',
  'Adventurous (15)'],
 'São Paulo': ['Shopping (257)',
  'Sights & Landmarks (246)',
  'Nightlife (246)',
  'Concerts & Shows (233)',
  'Museums (191)',
  'Spas & Wellness (187)',
  'Fun & Games (167)',
  'Tours (140)',
  'Outdoor Activities (107)',
  'Nature & Parks (86)',
  'Transportation (61)',
  'Food & Drink (42)',
  'Traveler Resources (33)',
  'Classes & Workshops (28)',
  'Boat Tours & Water Sports (17)',
  'See all',
  'Jardins (128)',
  'Pinheiros (120)',
  'Bela Vista (96)',
  'Consolacao (60)',
  'Republica (42)',
  'Centro (38)',
  'Vila Mariana (37)',
  'Butanta (29)',
  'Liberdade (25)',
  'Vila Madalena (22)',
  'Vila Buarque (21)',
  'Se (18)',
  'Itaim Bibi (16)',
  'Higienopolis (15)',
  'Ipiranga (14)',
  'See all',
  'Good for a Rainy Day (204)',
  'Good for Kids (182)',
  'Budget-friendly (170)',
  'Free Entry (159)',
  'Good for Big Groups (110)',
  'Good for Couples (95)',
  'Good for Adrenaline Seekers (37)',
  'Hidden Gems (13)',
  'Adventurous (8)',
  'Honeymoon spot (7)'],
 'Hamburg': ['Nightlife (259)',
  'Tours (163)',
  'Sights & Landmarks (148)',
  'Shopping (101)',
  'Museums (79)',
  'Outdoor Activities (74)',
  'Fun & Games (64)',
  'Concerts & Shows (57)',
  'Nature & Parks (48)',
  'Spas & Wellness (36)',
  'Boat Tours & Water Sports (34)',
  'Food & Drink (20)',
  'Classes & Workshops (13)',
  'Transportation (9)',
  'Traveler Resources (4)',
  'See all',
  'Good for a Rainy Day (114)',
  'Free Entry (81)',
  'Good for Big Groups (75)',
  'Budget-friendly (71)',
  'Good for Couples (62)',
  'Good for Kids (49)',
  'Honeymoon spot (23)',
  'Good for Adrenaline Seekers (21)',
  'Hidden Gems (17)',
  'Adventurous (15)'],
 'Milano': ['Sights & Landmarks (684)',
  'Shopping (358)',
  'Nightlife (303)',
  'Tours (212)',
  'Museums (191)',
  'Spas & Wellness (170)',
  'Food & Drink (103)',
  'Fun & Games (90)',
  'Nature & Parks (75)',
  'Transportation (72)',
  'Concerts & Shows (66)',
  'Outdoor Activities (66)',
  'Traveler Resources (59)',
  'Classes & Workshops (41)',
  'Day Trips (27)',
  'See all',
  'Centro Storico (886)',
  'Zone 3 (199)',
  'Zone 8 (137)',
  'Zone 9 (130)',
  'Zone 2 (126)',
  'Zone 6 (125)',
  'Zone 4 (107)',
  'Zone 5 (85)',
  'Ticinese (84)',
  'Zone 7 (64)',
  'Navigli (57)',
  'Porta Garibaldi (56)',
  'Porta Nuova (53)',
  "Quadrilatero della Moda (Quad d'Oro) (49)",
  'Porta Venezia (47)',
  'See all',
  'Good for a Rainy Day (234)',
  'Budget-friendly (179)',
  'Good for Couples (164)',
  'Free Entry (153)',
  'Good for Kids (129)',
  'Good for Big Groups (119)',
  'Hidden Gems (57)',
  'Honeymoon spot (36)',
  'Good for Adrenaline Seekers (16)',
  'Adventurous (11)'],{'Munich': ['Sights & Landmarks (226)',
  'Tours (168)',
  'Nightlife (152)',
  'Shopping (105)',
  'Museums (69)',
  'Outdoor Activities (66)',
  'Fun & Games (59)',
  'Spas & Wellness (51)',
  'Food & Drink (41)',
  'Concerts & Shows (37)',
  'Transportation (33)',
  'Nature & Parks (26)',
  'Day Trips (21)',
  'Classes & Workshops (19)',
  'Boat Tours & Water Sports (11)',
  'See all',
  'Good for a Rainy Day (127)',
  'Good for Couples (122)',
  'Budget-friendly (108)',
  'Free Entry (106)',
  'Good for Big Groups (103)',
  'Good for Kids (81)',
  'Honeymoon spot (40)',
  'Good for Adrenaline Seekers (18)',
  'Adventurous (16)',
  'Hidden Gems (16)'],
 'Buenos Aires': ['Sights & Landmarks (470)',
  'Tours (418)',
  'Shopping (277)',
  'Nightlife (226)',
  'Concerts & Shows (175)',
  'Museums (163)',
  'Outdoor Activities (158)',
  'Spas & Wellness (152)',
  'Classes & Workshops (119)',
  'Fun & Games (112)',
  'Transportation (94)',
  'Food & Drink (92)',
  'Nature & Parks (78)',
  'Boat Tours & Water Sports (50)',
  'Traveler Resources (15)',
  'See all',
  'El Centro (Downtown) (547)',
  'Palermo (331)',
  'San Nicolas (199)',
  'Recoleta (170)',
  'Microcentro (160)',
  'Montserrat (138)',
  'Retiro (131)',
  'Theater District (109)',
  'Palermo Soho (98)',
  'Balvanera (84)',
  'San Telmo (78)',
  'Palermo Hollywood (57)',
  'Belgrano (54)',
  'Caballito (53)',
  'Villa Crespo (49)',
  'See all',
  'Good for a Rainy Day (267)',
  'Good for Couples (249)',
  'Budget-friendly (249)',
  'Good for Big Groups (200)',
  'Free Entry (179)',
  'Good for Kids (153)','Honeymoon spot (86)','Good for Adrenaline Seekers (50)','Hidden Gems (32)', 'Adventurous (15)']}
```


      File "<ipython-input-5-59f9aba36c95>", line 802
        'Good for Kids (153)','Honeymoon spot (86)','Good for Adrenaline Seekers (50)','Hidden Gems (32)', 'Adventurous (15)']}
                                                                                                                               ^
    SyntaxError: unexpected EOF while parsing
    



```python
dikt3={'Singapore': ['Shopping (492)',
  'Spas & Wellness (453)',
  'Sights & Landmarks (327)',
  'Tours (276)',
  'Outdoor Activities (195)',
  'Fun & Games (190)',
  'Nightlife (171)',
  'Museums (126)',
  'Transportation (124)',
  'Classes & Workshops (124)',
  'Nature & Parks (121)',
  'Food & Drink (116)',
  'Boat Tours & Water Sports (74)',
  'Concerts & Shows (44)',
  'Events (21)',
  'See all',
  'Central Area/City Area (1,038)',
  'Downtown Core/Downtown Singapore (288)',
  'Central Business District (194)',
  'Rochor (187)',
  'Orchard (182)',
  'Outram (179)',
  'Orchard Road (177)',
  'Chinatown (133)',
  'Colonial District/Civic District (106)',
  'Marina Bay (105)',
  'Boulevard (103)',
  'Singapore River/Riverside (102)',
  'Bukit Merah (94)',
  'Kallang (91)',
  'City Hall (82)',
  'See all',
  'Good for a Rainy Day (382)',
  'Free Entry (372)',
  'Budget-friendly (276)',
  'Good for Couples (259)',
  'Good for Big Groups (229)',
  'Good for Kids (211)',
  'Hidden Gems (80)',
  'Honeymoon spot (58)',
  'Good for Adrenaline Seekers (48)',
  'Adventurous (30)'],
 'Vancouver': ['Spas & Wellness (224)',
  'Tours (216)',
  'Outdoor Activities (178)',
  'Shopping (157)',
  'Sights & Landmarks (106)',
  'Nightlife (92)',
  'Food & Drink (70)',
  'Boat Tours & Water Sports (67)',
  'Museums (66)',
  'Nature & Parks (61)',
  'Fun & Games (56)',
  'Transportation (52)',
  'Concerts & Shows (51)',
  'Classes & Workshops (24)',
  'Day Trips (19)',
  'See all',
  'Central (457)',
  'Downtown (356)',
  'East Vancouver (145)',
  'False Creek (113)',
  'Fairview (113)',
  'Granville Street (88)',
  'Granville Island & Fairview (77)',
  'West End (76)',
  'Robson Street (74)',
  'Kitsilano (72)',
  'Coal Harbour (70)',
  'Yaletown & False Creek North (69)',
  'Gastown (66)',
  'Granville Island (59)',
  'Yaletown (51)',
  'See all',
  'Good for Couples (221)',
  'Good for a Rainy Day (186)',
  'Budget-friendly (156)',
  'Good for Big Groups (144)',
  'Free Entry (125)',
  'Good for Kids (109)',
  'Hidden Gems (54)',
  'Honeymoon spot (53)',
  'Good for Adrenaline Seekers (46)',
  'Adventurous (28)'],
 'London': ['Nightlife (1,223)',
  'Tours (1,034)',
  'Sights & Landmarks (977)',
  'Shopping (938)',
  'Spas & Wellness (790)',
  'Fun & Games (526)',
  'Concerts & Shows (420)',
  'Museums (410)',
  'Transportation (407)',
  'Outdoor Activities (298)',
  'Food & Drink (296)',
  'Classes & Workshops (293)',
  'Nature & Parks (257)',
  'Boat Tours & Water Sports (93)',
  'Day Trips (65)',
  'See all',
  'Soho (262)',
  'City of London (261)',
  'Mayfair (225)',
  'Covent Garden (211)',
  'Westminster (163)',
  'Trafalgar Square / Embankment (139)',
  'Marylebone (134)',
  'Bloomsbury (121)',
  'Southwark (113)',
  'Notting Hill (106)',
  'Holborn (105)',
  'Shoreditch (98)',
  'Chelsea (94)',
  'Fitzrovia (86)',
  "St. James's (84)",
  'See all',
  'Good for a Rainy Day (1,650)',
  'Good for Couples (1,351)',
  'Free Entry (1,123)',
  'Budget-friendly (938)',
  'Good for Big Groups (921)',
  'Good for Kids (537)',
  'Hidden Gems (521)',
  'Adventurous (175)',
  'Honeymoon spot (147)',
  'Good for Adrenaline Seekers (124)'],
 'Toronto': ['Spas & Wellness (334)',
  'Shopping (238)',
  'Nightlife (207)',
  'Tours (203)',
  'Fun & Games (184)',
  'Sights & Landmarks (181)',
  'Outdoor Activities (146)',
  'Nature & Parks (114)',
  'Museums (110)',
  'Concerts & Shows (97)',
  'Food & Drink (72)',
  'Transportation (70)',
  'Classes & Workshops (58)',
  'Boat Tours & Water Sports (47)',
  'Day Trips (26)',
  'See all',
  'Old Toronto (1,089)',
  'Downtown (639)',
  'Waterfront Communities-The Island (225)',
  'Downtown West (200)',
  'Midtown (167)',
  'West End (130)',
  'Entertainment District (126)',
  'North York (126)',
  'Etobicoke (116)',
  'East End (111)',
  'Church-Yonge Corridor (103)',
  'Bay Street Corridor (98)',
  'Annex (87)',
  'Scarborough (86)',
  'Kensington-Chinatown (66)',
  'See all',
  'Good for a Rainy Day (269)',
  'Good for Couples (269)',
  'Good for Big Groups (211)',
  'Budget-friendly (170)',
  'Free Entry (165)',
  'Good for Kids (120)',
  'Hidden Gems (64)',
  'Honeymoon spot (52)',
  'Good for Adrenaline Seekers (43)',
  'Adventurous (33)'],
 'Budapest': ['Tours (427)',
  'Sights & Landmarks (330)',
  'Nightlife (281)',
  'Shopping (263)',
  'Fun & Games (201)',
  'Outdoor Activities (150)',
  'Spas & Wellness (141)',
  'Museums (135)',
  'Food & Drink (131)',
  'Transportation (79)',
  'Concerts & Shows (61)',
  'Nature & Parks (43)',
  'Classes & Workshops (41)',
  'Boat Tours & Water Sports (37)',
  'Traveler Resources (7)',
  'See all',
  'District V / Inner City (297)',
  'District VII / Jewish Quarter (194)',
  'District I / Buda (147)',
  'Várkerület (33)',
  'Gellert Hill (30)',
  'Belváros-Lipótváros (18)',
  'Terézváros (13)',
  'Margaret Island (8)',
  'Erzsébetváros (7)',
  'Óbuda-Békásmegyer (6)',
  'Zugló (5)',
  'Kispest (5)',
  'Andrássy út (4)',
  'Városliget (4)',
  'Sasad (3)',
  'See all',
  'Good for a Rainy Day (335)',
  'Good for Couples (330)',
  'Budget-friendly (313)',
  'Good for Big Groups (281)',
  'Free Entry (183)',
  'Good for Kids (171)',
  'Hidden Gems (124)',
  'Honeymoon spot (95)',
  'Good for Adrenaline Seekers (70)',
  'Adventurous (47)'],
 'Hong Kong': ['Shopping (485)',
  'Sights & Landmarks (350)',
  'Tours (251)',
  'Outdoor Activities (195)',
  'Nature & Parks (174)',
  'Spas & Wellness (145)',
  'Museums (112)',
  'Fun & Games (100)',
  'Nightlife (96)',
  'Food & Drink (91)',
  'Classes & Workshops (69)',
  'Boat Tours & Water Sports (67)',
  'Transportation (48)',
  'Concerts & Shows (23)',
  'Events (18)',
  'See all',
  'Hong Kong Island (436)',
  'Kowloon (242)',
  'New Territories (232)',
  'Central District (224)',
  'Yau Tsim Mong District (171)',
  'Central (135)',
  'Tsim Sha Tsui (95)',
  'Southern District (50)',
  'Islands District (50)',
  'Sheung Wan (49)',
  'Mong Kok (39)',
  'Eastern District (36)',
  'Sai Kung (35)',
  'Yuen Long (34)',
  'Sha Tin (34)',
  'See all',
  'Free Entry (381)',
  'Budget-friendly (257)',
  'Good for a Rainy Day (252)',
  'Good for Couples (234)',
  'Good for Kids (203)',
  'Good for Big Groups (134)',
  'Hidden Gems (57)',
  'Honeymoon spot (40)',
  'Good for Adrenaline Seekers (22)',
  'Adventurous (14)'],
 'Stockholm': ['Tours (140)',
  'Sights & Landmarks (119)',
  'Outdoor Activities (101)',
  'Shopping (86)',
  'Museums (77)',
  'Fun & Games (64)',
  'Nature & Parks (60)',
  'Boat Tours & Water Sports (50)',
  'Nightlife (40)',
  'Spas & Wellness (39)',
  'Concerts & Shows (28)',
  'Transportation (21)',
  'Food & Drink (21)',
  'Classes & Workshops (10)',
  'Traveler Resources (9)',
  'See all',
  'Norrmalm (120)',
  'Sodermalm Borough (87)',
  'Sodermalm (82)',
  'Gamla Stan & Riddarholmen (80)',
  'Ostermalm (78)',
  'Kungsholmen (32)',
  'Vasastan (32)',
  'Djurgarden & Djurgardsbrunn (32)',
  'SoFo & Medborgarplatsen (25)',
  'Enskede-Arsta-Vantor Borough (20)',
  'Mariatorget (16)',
  'Hornstull & Langholmen (13)',
  'Johanneshov (10)',
  'Slussen (10)',
  'Skeppsholmen (8)',
  'See all',
  'Good for a Rainy Day (141)',
  'Budget-friendly (127)',
  'Good for Couples (114)',
  'Good for Kids (82)',
  'Free Entry (80)',
  'Good for Big Groups (79)',
  'Hidden Gems (36)',
  'Honeymoon spot (30)',
  'Good for Adrenaline Seekers (17)',
  'Adventurous (16)'],
 'Sydney': ['Tours (510)',
  'Outdoor Activities (336)',
  'Spas & Wellness (282)',
  'Nightlife (218)',
  'Shopping (214)',
  'Sights & Landmarks (187)',
  'Boat Tours & Water Sports (152)',
  'Nature & Parks (143)',
  'Food & Drink (130)',
  'Fun & Games (128)',
  'Transportation (110)',
  'Museums (99)',
  'Concerts & Shows (57)',
  'Classes & Workshops (57)',
  'Day Trips (37)',
  'See all',
  'Central Business District (367)',
  'The Rocks (81)',
  'Surry Hills (60)',
  'Darlinghurst (53)',
  'Paddington (46)',
  'Darling Harbour (44)',
  'Newtown (43)',
  'Balmain (30)',
  'Double Bay (26)',
  'Chinatown (21)',
  'Glebe (18)',
  'Inner West (12)',
  'Inner East (11)',
  'Manly (10)',
  'Mosman (10)',
  'See all',
  'Good for Big Groups (348)',
  'Good for Couples (334)',
  'Good for a Rainy Day (277)',
  'Budget-friendly (274)',
  'Free Entry (255)',
  'Good for Kids (187)',
  'Honeymoon spot (90)',
  'Hidden Gems (87)',
  'Good for Adrenaline Seekers (74)',
  'Adventurous (64)'],
 'Kuala Lumpur': ['Tours (193)',
  'Shopping (155)',
  'Spas & Wellness (147)',
  'Transportation (137)',
  'Sights & Landmarks (106)',
  'Outdoor Activities (95)',
  'Nightlife (93)',
  'Day Trips (76)',
  'Fun & Games (65)',
  'Museums (53)',
  'Food & Drink (47)',
  'Classes & Workshops (46)',
  'Nature & Parks (35)',
  'Concerts & Shows (18)',
  'Boat Tours & Water Sports (14)',
  'See all',
  'Good for a Rainy Day (188)',
  'Free Entry (154)',
  'Budget-friendly (150)',
  'Good for Couples (149)',
  'Good for Big Groups (130)',
  'Good for Kids (119)',
  'Hidden Gems (29)',
  'Honeymoon spot (26)',
  'Good for Adrenaline Seekers (24)',
  'Adventurous (14)'],
 'Barcelona': ['Tours (823)',
  'Nightlife (594)',
  'Spas & Wellness (560)',
  'Sights & Landmarks (511)',
  'Outdoor Activities (443)',
  'Shopping (426)',
  'Food & Drink (256)',
  'Fun & Games (210)',
  'Museums (165)',
  'Classes & Workshops (150)',
  'Boat Tours & Water Sports (126)',
  'Transportation (118)',
  'Concerts & Shows (116)',
  'Nature & Parks (115)',
  'Day Trips (63)',
  'See all',
  'Ciutat Vella (Old Town) (956)',
  'Eixample (742)',
  'Barrio Gotico (Barri Gotic) (419)',
  "La Dreta de l'Eixample (315)",
  'Sant Marti (265)',
  'Sant Pere, Santa Caterina i la Ribera (248)',
  'El Born / La Ribera (222)',
  'El Raval (211)',
  'Gracia (197)',
  "L'Antiga Esquerra de l'Eixample (167)",
  'Vila de Gracia (144)',
  'Ciutadella / Vila Olimpica (138)',
  'Sant Gervasi-Galvany (103)',
  'La Rambla (102)',
  'Les Corts (94)',
  'See all',
  'Good for Couples (503)',
  'Good for a Rainy Day (466)',
  'Budget-friendly (450)',
  'Good for Big Groups (358)',
  'Good for Kids (271)',
  'Free Entry (241)',
  'Hidden Gems (201)',
  'Honeymoon spot (201)',
  'Good for Adrenaline Seekers (129)',
  'Adventurous (54)'],
 'Paris': ['Sights & Landmarks (1,880)',
  'Spas & Wellness (932)',
  'Shopping (842)',
  'Tours (834)',
  'Nightlife (497)',
  'Museums (281)',
  'Transportation (275)',
  'Concerts & Shows (270)',
  'Fun & Games (262)',
  'Food & Drink (251)',
  'Nature & Parks (242)',
  'Outdoor Activities (222)',
  'Classes & Workshops (218)',
  'Day Trips (63)',
  'Traveler Resources (60)',
  'See all',
  'Opera / Bourse (502)',
  '1st Arr. - Louvre (377)',
  '8th Arr. - Elysee (373)',
  '6th Arr. - Luxembourg (345)',
  'Le Marais (341)',
  '16th Arr. - Passy (317)',
  '9th Arr. - Opera (308)',
  '4th Arr. - Hotel-de-Ville (300)',
  '11th Arr. - Popincourt (297)',
  'Louvre / Palais-Royal (281)',
  '5th Arr. - Pantheon (270)',
  'Quartier Latin (267)',
  'Champs-Elysees (260)',
  '7th Arr. - Palais-Bourbon (258)',
  '15th Arr. - Vaugirard (239)',
  'See all',
  'Good for a Rainy Day (717)',
  'Good for Couples (599)',
  'Budget-friendly (433)',
  'Good for Kids (396)',
  'Free Entry (377)',
  'Good for Big Groups (321)',
  'Honeymoon spot (222)',
  'Hidden Gems (221)',
  'Good for Adrenaline Seekers (52)',
  'Adventurous (15)'], 'Berlin': ['Nightlife (560)',
  'Tours (493)',
  'Sights & Landmarks (477)',
  'Shopping (323)',
  'Spas & Wellness (314)',
  'Museums (257)',
  'Outdoor Activities (198)',
  'Fun & Games (175)',
  'Concerts & Shows (132)',
  'Nature & Parks (81)',
  'Food & Drink (68)',
  'Boat Tours & Water Sports (62)',
  'Classes & Workshops (53)',
  'Traveler Resources (52)',
  'Transportation (29)',
  'See all',
  'Mitte (Borough) (890)',
  'Mitte (637)',
  'Friedrichshain-Kreuzberg (Borough) (386)',
  'Charlottenburg-Wilmersdorf (Borough) (356)',
  'Pankow (Borough) (248)',
  'Charlottenburg (224)',
  'Kreuzberg (219)',
  'Prenzlauer Berg (206)',
  'Friedrichshain (165)',
  'Tempelhof-Schoneberg (Borough) (145)',
  'Tiergarten (135)',
  'Neukolln (Borough) (121)',
  'Neukolln (110)',
  'Schoneberg (94)',
  'Steglitz-Zehlendorf (Borough) (89)',
  'See all',
  'Good for a Rainy Day (380)',
  'Good for Couples (309)',
  'Budget-friendly (283)',
  'Free Entry (255)',
  'Good for Big Groups (239)',
  'Good for Kids (128)',
  'Hidden Gems (111)',
  'Good for Adrenaline Seekers (51)',
  'Honeymoon spot (50)',
  'Adventurous (38)'],
 'Ottawa': ['Sights & Landmarks (96)',
  'Fun & Games (89)',
  'Shopping (77)',
  'Outdoor Activities (76)',
  'Tours (66)',
  'Nightlife (64)',
  'Nature & Parks (59)',
  'Spas & Wellness (56)',
  'Museums (41)',
  'Food & Drink (33)',
  'Concerts & Shows (28)',
  'Boat Tours & Water Sports (21)',
  'Classes & Workshops (12)',
  'Transportation (11)',
  'Traveler Resources (6)',
  'See all',
  'Good for Couples (123)',
  'Good for a Rainy Day (115)',
  'Good for Big Groups (109)',
  'Budget-friendly (104)',
  'Good for Kids (84)',
  'Free Entry (78)',
  'Hidden Gems (28)',
  'Honeymoon spot (19)',
  'Good for Adrenaline Seekers (19)',
  'Adventurous (14)'],
 'Melbourne': ['Tours (388)',
  'Sights & Landmarks (211)',
  'Outdoor Activities (204)',
  'Nightlife (168)',
  'Shopping (163)',
  'Food & Drink (135)',
  'Spas & Wellness (119)',
  'Nature & Parks (112)',
  'Fun & Games (112)',
  'Transportation (97)',
  'Day Trips (71)',
  'Museums (64)',
  'Boat Tours & Water Sports (48)',
  'Concerts & Shows (47)',
  'Classes & Workshops (36)',
  'See all',
  'Central Business District (433)',
  'Chinatown (57)',
  'Southbank (41)',
  'South Melbourne (27)',
  'Docklands (19)',
  'Lygon Street (16)',
  'Chapel Street (15)',
  'Port Melbourne (8)',
  'Parkville (7)',
  'North Melbourne (3)',
  'Fitzroy (3)',
  'Middle Park (1)',
  'Good for Couples (270)',
  'Good for a Rainy Day (270)',
  'Good for Big Groups (266)',
  'Budget-friendly (205)',
  'Free Entry (189)',
  'Good for Kids (132)',
  'Honeymoon spot (66)',
  'Hidden Gems (63)',
  'Adventurous (37)',
  'Good for Adrenaline Seekers (36)'],
 'Zurich': ['Spas & Wellness (143)',
  'Nightlife (110)',
  'Tours (84)',
  'Shopping (83)',
  'Museums (67)',
  'Sights & Landmarks (65)',
  'Outdoor Activities (44)',
  'Transportation (40)',
  'Fun & Games (38)',
  'Nature & Parks (27)',
  'Day Trips (24)',
  'Food & Drink (22)',
  'Classes & Workshops (19)',
  'Concerts & Shows (16)',
  'Boat Tours & Water Sports (13)',
  'See all',
  'Good for a Rainy Day (94)',
  'Free Entry (63)',
  'Good for Couples (57)',
  'Budget-friendly (52)',
  'Good for Big Groups (48)',
  'Good for Kids (44)',
  'Hidden Gems (20)',
  'Honeymoon spot (15)',
  'Good for Adrenaline Seekers (9)',
  'Adventurous (6)'],
 'Oslo': ['Sights & Landmarks (163)',
  'Museums (108)',
  'Shopping (106)',
  'Nightlife (91)',
  'Outdoor Activities (74)',
  'Tours (73)',
  'Fun & Games (67)',
  'Nature & Parks (64)',
  'Spas & Wellness (34)',
  'Concerts & Shows (29)',
  'Boat Tours & Water Sports (21)',
  'Food & Drink (17)',
  'Transportation (11)',
  'Classes & Workshops (11)',
  'Traveler Resources (8)',
  'See all',
  'Good for a Rainy Day (103)',
  'Good for Big Groups (85)',
  'Good for Couples (84)',
  'Budget-friendly (83)',
  'Free Entry (81)',
  'Good for Kids (71)',
  'Hidden Gems (41)',
  'Good for Adrenaline Seekers (21)',
  'Adventurous (16)',
  'Honeymoon spot (16)'],
 'Helsinki': ['Shopping (133)',
  'Sights & Landmarks (119)',
  'Tours (109)',
  'Outdoor Activities (88)',
  'Museums (77)',
  'Nightlife (77)',
  'Fun & Games (66)',
  'Nature & Parks (51)',
  'Spas & Wellness (40)',
  'Boat Tours & Water Sports (30)',
  'Transportation (19)',
  'Concerts & Shows (19)',
  'Food & Drink (12)',
  'Day Trips (9)',
  'Traveler Resources (7)',
  'See all',
  'Good for a Rainy Day (138)',
  'Budget-friendly (102)',
  'Free Entry (96)',
  'Good for Big Groups (83)',
  'Good for Kids (78)',
  'Good for Couples (73)',
  'Hidden Gems (31)',
  'Good for Adrenaline Seekers (21)',
  'Honeymoon spot (17)',
  'Adventurous (15)'],
 'São Paulo': ['Shopping (257)',
  'Sights & Landmarks (246)',
  'Nightlife (246)',
  'Concerts & Shows (233)',
  'Museums (191)',
  'Spas & Wellness (187)',
  'Fun & Games (167)',
  'Tours (140)',
  'Outdoor Activities (107)',
  'Nature & Parks (86)',
  'Transportation (61)',
  'Food & Drink (42)',
  'Traveler Resources (33)',
  'Classes & Workshops (28)',
  'Boat Tours & Water Sports (17)',
  'See all',
  'Jardins (128)',
  'Pinheiros (120)',
  'Bela Vista (96)',
  'Consolacao (60)',
  'Republica (42)',
  'Centro (38)',
  'Vila Mariana (37)',
  'Butanta (29)',
  'Liberdade (25)',
  'Vila Madalena (22)',
  'Vila Buarque (21)',
  'Se (18)',
  'Itaim Bibi (16)',
  'Higienopolis (15)',
  'Ipiranga (14)',
  'See all',
  'Good for a Rainy Day (204)',
  'Good for Kids (182)',
  'Budget-friendly (170)',
  'Free Entry (159)',
  'Good for Big Groups (110)',
  'Good for Couples (95)',
  'Good for Adrenaline Seekers (37)',
  'Hidden Gems (13)',
  'Adventurous (8)',
  'Honeymoon spot (7)'],
 'Hamburg': ['Nightlife (259)',
  'Tours (163)',
  'Sights & Landmarks (148)',
  'Shopping (101)',
  'Museums (79)',
  'Outdoor Activities (74)',
  'Fun & Games (64)',
  'Concerts & Shows (57)',
  'Nature & Parks (48)',
  'Spas & Wellness (36)',
  'Boat Tours & Water Sports (34)',
  'Food & Drink (20)',
  'Classes & Workshops (13)',
  'Transportation (9)',
  'Traveler Resources (4)',
  'See all',
  'Good for a Rainy Day (114)',
  'Free Entry (81)',
  'Good for Big Groups (75)',
  'Budget-friendly (71)',
  'Good for Couples (62)',
  'Good for Kids (49)',
  'Honeymoon spot (23)',
  'Good for Adrenaline Seekers (21)',
  'Hidden Gems (17)',
  'Adventurous (15)'],
 'Milano': ['Sights & Landmarks (684)',
  'Shopping (358)',
  'Nightlife (303)',
  'Tours (212)',
  'Museums (191)',
  'Spas & Wellness (170)',
  'Food & Drink (103)',
  'Fun & Games (90)',
  'Nature & Parks (75)',
  'Transportation (72)',
  'Concerts & Shows (66)',
  'Outdoor Activities (66)',
  'Traveler Resources (59)',
  'Classes & Workshops (41)',
  'Day Trips (27)',
  'See all',
  'Centro Storico (886)',
  'Zone 3 (199)',
  'Zone 8 (137)',
  'Zone 9 (130)',
  'Zone 2 (126)',
  'Zone 6 (125)',
  'Zone 4 (107)',
  'Zone 5 (85)',
  'Ticinese (84)',
  'Zone 7 (64)',
  'Navigli (57)',
  'Porta Garibaldi (56)',
  'Porta Nuova (53)',
  "Quadrilatero della Moda (Quad d'Oro) (49)",
  'Porta Venezia (47)',
  'See all',
  'Good for a Rainy Day (234)',
  'Budget-friendly (179)',
  'Good for Couples (164)',
  'Free Entry (153)',
  'Good for Kids (129)',
  'Good for Big Groups (119)',
  'Hidden Gems (57)',
  'Honeymoon spot (36)',
  'Good for Adrenaline Seekers (16)',
  'Adventurous (11)'],{'Munich': ['Sights & Landmarks (226)',
  'Tours (168)',
  'Nightlife (152)',
  'Shopping (105)',
  'Museums (69)',
  'Outdoor Activities (66)',
  'Fun & Games (59)',
  'Spas & Wellness (51)',
  'Food & Drink (41)',
  'Concerts & Shows (37)',
  'Transportation (33)',
  'Nature & Parks (26)',
  'Day Trips (21)',
  'Classes & Workshops (19)',
  'Boat Tours & Water Sports (11)',
  'See all',
  'Good for a Rainy Day (127)',
  'Good for Couples (122)',
  'Budget-friendly (108)',
  'Free Entry (106)',
  'Good for Big Groups (103)',
  'Good for Kids (81)',
  'Honeymoon spot (40)',
  'Good for Adrenaline Seekers (18)',
  'Adventurous (16)',
  'Hidden Gems (16)'],
 'Buenos Aires': ['Sights & Landmarks (470)',
  'Tours (418)',
  'Shopping (277)',
  'Nightlife (226)',
  'Concerts & Shows (175)',
  'Museums (163)',
  'Outdoor Activities (158)',
  'Spas & Wellness (152)',
  'Classes & Workshops (119)',
  'Fun & Games (112)',
  'Transportation (94)',
  'Food & Drink (92)',
  'Nature & Parks (78)',
  'Boat Tours & Water Sports (50)',
  'Traveler Resources (15)',
  'See all',
  'El Centro (Downtown) (547)',
  'Palermo (331)',
  'San Nicolas (199)',
  'Recoleta (170)',
  'Microcentro (160)',
  'Montserrat (138)',
  'Retiro (131)',
  'Theater District (109)',
  'Palermo Soho (98)',
  'Balvanera (84)',
  'San Telmo (78)',
  'Palermo Hollywood (57)',
  'Belgrano (54)',
  'Caballito (53)',
  'Villa Crespo (49)',
  'See all',
  'Good for a Rainy Day (267)',
  'Good for Couples (249)',
  'Budget-friendly (249)',
  'Good for Big Groups (200)',
  'Free Entry (179)',
  'Good for Kids (153)','Honeymoon spot (86)','Good for Adrenaline Seekers (50)','Hidden Gems (32)', 'Adventurous (15)']}
```


      File "<ipython-input-7-59f9aba36c95>", line 802
        'Good for Kids (153)','Honeymoon spot (86)','Good for Adrenaline Seekers (50)','Hidden Gems (32)', 'Adventurous (15)']}
                                                                                                                               ^
    SyntaxError: unexpected EOF while parsing
    



```python
dikt3={'Singapore': ['Shopping (492)', 'Spas & Wellness (453)', 'Sights & Landmarks (327)', 'Tours (276)', 'Outdoor Activities (195)', 'Fun & Games (190)', 'Nightlife (171)', 'Museums (126)', 'Transportation (124)', 'Classes & Workshops (124)', 'Nature & Parks (121)', 'Food & Drink (116)', 'Boat Tours & Water Sports (74)', 'Concerts & Shows (44)', 'Events (21)', 'See all', 'Central Area/City Area (1,038)', 'Downtown Core/Downtown Singapore (288)', 'Central Business District (194)', 'Rochor (187)', 'Orchard (182)', 'Outram (179)', 'Orchard Road (177)', 'Chinatown (133)', 'Colonial District/Civic District (106)', 'Marina Bay (105)', 'Boulevard (103)', 'Singapore River/Riverside (102)', 'Bukit Merah (94)', 'Kallang (91)', 'City Hall (82)', 'See all', 'Good for a Rainy Day (382)', 'Free Entry (372)', 'Budget-friendly (276)', 'Good for Couples (259)', 'Good for Big Groups (229)', 'Good for Kids (211)', 'Hidden Gems (80)', 'Honeymoon spot (58)', 'Good for Adrenaline Seekers (48)', 'Adventurous (30)'], 'Vancouver': ['Spas & Wellness (224)', 'Tours (216)', 'Outdoor Activities (178)', 'Shopping (157)', 'Sights & Landmarks (106)', 'Nightlife (92)', 'Food & Drink (70)', 'Boat Tours & Water Sports (67)', 'Museums (66)', 'Nature & Parks (61)', 'Fun & Games (56)', 'Transportation (52)', 'Concerts & Shows (51)', 'Classes & Workshops (24)', 'Day Trips (19)', 'See all', 'Central (457)', 'Downtown (356)', 'East Vancouver (145)', 'False Creek (113)', 'Fairview (113)', 'Granville Street (88)', 'Granville Island & Fairview (77)', 'West End (76)', 'Robson Street (74)', 'Kitsilano (72)', 'Coal Harbour (70)', 'Yaletown & False Creek North (69)', 'Gastown (66)', 'Granville Island (59)', 'Yaletown (51)', 'See all', 'Good for Couples (221)', 'Good for a Rainy Day (186)', 'Budget-friendly (156)', 'Good for Big Groups (144)', 'Free Entry (125)', 'Good for Kids (109)', 'Hidden Gems (54)', 'Honeymoon spot (53)', 'Good for Adrenaline Seekers (46)', 'Adventurous (28)'], 'London': ['Nightlife (1,223)', 'Tours (1,034)', 'Sights & Landmarks (977)', 'Shopping (938)', 'Spas & Wellness (790)', 'Fun & Games (526)', 'Concerts & Shows (420)', 'Museums (410)', 'Transportation (407)', 'Outdoor Activities (298)', 'Food & Drink (296)', 'Classes & Workshops (293)', 'Nature & Parks (257)', 'Boat Tours & Water Sports (93)', 'Day Trips (65)', 'See all', 'Soho (262)', 'City of London (261)', 'Mayfair (225)', 'Covent Garden (211)', 'Westminster (163)', 'Trafalgar Square / Embankment (139)', 'Marylebone (134)', 'Bloomsbury (121)', 'Southwark (113)', 'Notting Hill (106)', 'Holborn (105)', 'Shoreditch (98)', 'Chelsea (94)', 'Fitzrovia (86)', "St. James's (84)", 'See all', 'Good for a Rainy Day (1,650)', 'Good for Couples (1,351)', 'Free Entry (1,123)', 'Budget-friendly (938)', 'Good for Big Groups (921)', 'Good for Kids (537)', 'Hidden Gems (521)', 'Adventurous (175)', 'Honeymoon spot (147)', 'Good for Adrenaline Seekers (124)'], 'Toronto': ['Spas & Wellness (334)', 'Shopping (238)', 'Nightlife (207)', 'Tours (203)', 'Fun & Games (184)', 'Sights & Landmarks (181)', 'Outdoor Activities (146)', 'Nature & Parks (114)', 'Museums (110)', 'Concerts & Shows (97)', 'Food & Drink (72)', 'Transportation (70)', 'Classes & Workshops (58)', 'Boat Tours & Water Sports (47)', 'Day Trips (26)', 'See all', 'Old Toronto (1,089)', 'Downtown (639)', 'Waterfront Communities-The Island (225)', 'Downtown West (200)', 'Midtown (167)', 'West End (130)', 'Entertainment District (126)', 'North York (126)', 'Etobicoke (116)', 'East End (111)', 'Church-Yonge Corridor (103)', 'Bay Street Corridor (98)', 'Annex (87)', 'Scarborough (86)', 'Kensington-Chinatown (66)', 'See all', 'Good for a Rainy Day (269)', 'Good for Couples (269)', 'Good for Big Groups (211)', 'Budget-friendly (170)', 'Free Entry (165)', 'Good for Kids (120)', 'Hidden Gems (64)', 'Honeymoon spot (52)', 'Good for Adrenaline Seekers (43)', 'Adventurous (33)'], 'Budapest': ['Tours (427)', 'Sights & Landmarks (330)', 'Nightlife (281)', 'Shopping (263)', 'Fun & Games (201)', 'Outdoor Activities (150)', 'Spas & Wellness (141)', 'Museums (135)', 'Food & Drink (131)', 'Transportation (79)', 'Concerts & Shows (61)', 'Nature & Parks (43)', 'Classes & Workshops (41)', 'Boat Tours & Water Sports (37)', 'Traveler Resources (7)', 'See all', 'District V / Inner City (297)', 'District VII / Jewish Quarter (194)', 'District I / Buda (147)', 'Várkerület (33)', 'Gellert Hill (30)', 'Belváros-Lipótváros (18)', 'Terézváros (13)', 'Margaret Island (8)', 'Erzsébetváros (7)', 'Óbuda-Békásmegyer (6)', 'Zugló (5)', 'Kispest (5)', 'Andrássy út (4)', 'Városliget (4)', 'Sasad (3)', 'See all', 'Good for a Rainy Day (335)', 'Good for Couples (330)', 'Budget-friendly (313)', 'Good for Big Groups (281)', 'Free Entry (183)', 'Good for Kids (171)', 'Hidden Gems (124)', 'Honeymoon spot (95)', 'Good for Adrenaline Seekers (70)', 'Adventurous (47)'], 'Hong Kong': ['Shopping (485)', 'Sights & Landmarks (350)', 'Tours (251)', 'Outdoor Activities (195)', 'Nature & Parks (174)', 'Spas & Wellness (145)', 'Museums (112)', 'Fun & Games (100)', 'Nightlife (96)', 'Food & Drink (91)', 'Classes & Workshops (69)', 'Boat Tours & Water Sports (67)', 'Transportation (48)', 'Concerts & Shows (23)', 'Events (18)', 'See all', 'Hong Kong Island (436)', 'Kowloon (242)', 'New Territories (232)', 'Central District (224)', 'Yau Tsim Mong District (171)', 'Central (135)', 'Tsim Sha Tsui (95)', 'Southern District (50)', 'Islands District (50)', 'Sheung Wan (49)', 'Mong Kok (39)', 'Eastern District (36)', 'Sai Kung (35)', 'Yuen Long (34)', 'Sha Tin (34)', 'See all', 'Free Entry (381)', 'Budget-friendly (257)', 'Good for a Rainy Day (252)', 'Good for Couples (234)', 'Good for Kids (203)', 'Good for Big Groups (134)', 'Hidden Gems (57)', 'Honeymoon spot (40)', 'Good for Adrenaline Seekers (22)', 'Adventurous (14)'], 'Stockholm': ['Tours (140)', 'Sights & Landmarks (119)', 'Outdoor Activities (101)', 'Shopping (86)', 'Museums (77)', 'Fun & Games (64)', 'Nature & Parks (60)', 'Boat Tours & Water Sports (50)', 'Nightlife (40)', 'Spas & Wellness (39)', 'Concerts & Shows (28)', 'Transportation (21)', 'Food & Drink (21)', 'Classes & Workshops (10)', 'Traveler Resources (9)', 'See all', 'Norrmalm (120)', 'Sodermalm Borough (87)', 'Sodermalm (82)', 'Gamla Stan & Riddarholmen (80)', 'Ostermalm (78)', 'Kungsholmen (32)', 'Vasastan (32)', 'Djurgarden & Djurgardsbrunn (32)', 'SoFo & Medborgarplatsen (25)', 'Enskede-Arsta-Vantor Borough (20)', 'Mariatorget (16)', 'Hornstull & Langholmen (13)', 'Johanneshov (10)', 'Slussen (10)', 'Skeppsholmen (8)', 'See all', 'Good for a Rainy Day (141)', 'Budget-friendly (127)', 'Good for Couples (114)', 'Good for Kids (82)', 'Free Entry (80)', 'Good for Big Groups (79)', 'Hidden Gems (36)', 'Honeymoon spot (30)', 'Good for Adrenaline Seekers (17)', 'Adventurous (16)'], 'Sydney': ['Tours (510)', 'Outdoor Activities (336)', 'Spas & Wellness (282)', 'Nightlife (218)', 'Shopping (214)', 'Sights & Landmarks (187)', 'Boat Tours & Water Sports (152)', 'Nature & Parks (143)', 'Food & Drink (130)', 'Fun & Games (128)', 'Transportation (110)', 'Museums (99)', 'Concerts & Shows (57)', 'Classes & Workshops (57)', 'Day Trips (37)', 'See all', 'Central Business District (367)', 'The Rocks (81)', 'Surry Hills (60)', 'Darlinghurst (53)', 'Paddington (46)', 'Darling Harbour (44)', 'Newtown (43)', 'Balmain (30)', 'Double Bay (26)', 'Chinatown (21)', 'Glebe (18)', 'Inner West (12)', 'Inner East (11)', 'Manly (10)', 'Mosman (10)', 'See all', 'Good for Big Groups (348)', 'Good for Couples (334)', 'Good for a Rainy Day (277)', 'Budget-friendly (274)', 'Free Entry (255)', 'Good for Kids (187)', 'Honeymoon spot (90)', 'Hidden Gems (87)', 'Good for Adrenaline Seekers (74)', 'Adventurous (64)'], 'Kuala Lumpur': ['Tours (193)', 'Shopping (155)', 'Spas & Wellness (147)', 'Transportation (137)', 'Sights & Landmarks (106)', 'Outdoor Activities (95)', 'Nightlife (93)', 'Day Trips (76)', 'Fun & Games (65)', 'Museums (53)', 'Food & Drink (47)', 'Classes & Workshops (46)', 'Nature & Parks (35)', 'Concerts & Shows (18)', 'Boat Tours & Water Sports (14)', 'See all', 'Good for a Rainy Day (188)', 'Free Entry (154)', 'Budget-friendly (150)', 'Good for Couples (149)', 'Good for Big Groups (130)', 'Good for Kids (119)', 'Hidden Gems (29)', 'Honeymoon spot (26)', 'Good for Adrenaline Seekers (24)', 'Adventurous (14)'], 'Barcelona': ['Tours (823)', 'Nightlife (594)', 'Spas & Wellness (560)', 'Sights & Landmarks (511)', 'Outdoor Activities (443)', 'Shopping (426)', 'Food & Drink (256)', 'Fun & Games (210)', 'Museums (165)', 'Classes & Workshops (150)', 'Boat Tours & Water Sports (126)', 'Transportation (118)', 'Concerts & Shows (116)', 'Nature & Parks (115)', 'Day Trips (63)', 'See all', 'Ciutat Vella (Old Town) (956)', 'Eixample (742)', 'Barrio Gotico (Barri Gotic) (419)', "La Dreta de l'Eixample (315)", 'Sant Marti (265)', 'Sant Pere, Santa Caterina i la Ribera (248)', 'El Born / La Ribera (222)', 'El Raval (211)', 'Gracia (197)', "L'Antiga Esquerra de l'Eixample (167)", 'Vila de Gracia (144)', 'Ciutadella / Vila Olimpica (138)', 'Sant Gervasi-Galvany (103)', 'La Rambla (102)', 'Les Corts (94)', 'See all', 'Good for Couples (503)', 'Good for a Rainy Day (466)', 'Budget-friendly (450)', 'Good for Big Groups (358)', 'Good for Kids (271)', 'Free Entry (241)', 'Hidden Gems (201)', 'Honeymoon spot (201)', 'Good for Adrenaline Seekers (129)', 'Adventurous (54)'], 'Paris': ['Sights & Landmarks (1,880)', 'Spas & Wellness (932)', 'Shopping (842)', 'Tours (834)', 'Nightlife (497)', 'Museums (281)', 'Transportation (275)', 'Concerts & Shows (270)', 'Fun & Games (262)', 'Food & Drink (251)', 'Nature & Parks (242)', 'Outdoor Activities (222)', 'Classes & Workshops (218)', 'Day Trips (63)', 'Traveler Resources (60)', 'See all', 'Opera / Bourse (502)', '1st Arr. - Louvre (377)', '8th Arr. - Elysee (373)', '6th Arr. - Luxembourg (345)', 'Le Marais (341)', '16th Arr. - Passy (317)', '9th Arr. - Opera (308)', '4th Arr. - Hotel-de-Ville (300)', '11th Arr. - Popincourt (297)', 'Louvre / Palais-Royal (281)', '5th Arr. - Pantheon (270)', 'Quartier Latin (267)', 'Champs-Elysees (260)', '7th Arr. - Palais-Bourbon (258)', '15th Arr. - Vaugirard (239)', 'See all', 'Good for a Rainy Day (717)', 'Good for Couples (599)', 'Budget-friendly (433)', 'Good for Kids (396)', 'Free Entry (377)', 'Good for Big Groups (321)', 'Honeymoon spot (222)', 'Hidden Gems (221)', 'Good for Adrenaline Seekers (52)', 'Adventurous (15)'], 'Berlin': ['Nightlife (560)', 'Tours (493)', 'Sights & Landmarks (477)', 'Shopping (323)', 'Spas & Wellness (314)', 'Museums (257)', 'Outdoor Activities (198)', 'Fun & Games (175)', 'Concerts & Shows (132)', 'Nature & Parks (81)', 'Food & Drink (68)', 'Boat Tours & Water Sports (62)', 'Classes & Workshops (53)', 'Traveler Resources (52)', 'Transportation (29)', 'See all', 'Mitte (Borough) (890)', 'Mitte (637)', 'Friedrichshain-Kreuzberg (Borough) (386)', 'Charlottenburg-Wilmersdorf (Borough) (356)', 'Pankow (Borough) (248)', 'Charlottenburg (224)', 'Kreuzberg (219)', 'Prenzlauer Berg (206)', 'Friedrichshain (165)', 'Tempelhof-Schoneberg (Borough) (145)', 'Tiergarten (135)', 'Neukolln (Borough) (121)', 'Neukolln (110)', 'Schoneberg (94)', 'Steglitz-Zehlendorf (Borough) (89)', 'See all', 'Good for a Rainy Day (380)', 'Good for Couples (309)', 'Budget-friendly (283)', 'Free Entry (255)', 'Good for Big Groups (239)', 'Good for Kids (128)', 'Hidden Gems (111)', 'Good for Adrenaline Seekers (51)', 'Honeymoon spot (50)', 'Adventurous (38)'], 'Ottawa': ['Sights & Landmarks (96)', 'Fun & Games (89)', 'Shopping (77)', 'Outdoor Activities (76)', 'Tours (66)', 'Nightlife (64)', 'Nature & Parks (59)', 'Spas & Wellness (56)', 'Museums (41)', 'Food & Drink (33)', 'Concerts & Shows (28)', 'Boat Tours & Water Sports (21)', 'Classes & Workshops (12)', 'Transportation (11)', 'Traveler Resources (6)', 'See all', 'Good for Couples (123)', 'Good for a Rainy Day (115)', 'Good for Big Groups (109)', 'Budget-friendly (104)', 'Good for Kids (84)', 'Free Entry (78)', 'Hidden Gems (28)', 'Honeymoon spot (19)', 'Good for Adrenaline Seekers (19)', 'Adventurous (14)'], 'Melbourne': ['Tours (388)', 'Sights & Landmarks (211)', 'Outdoor Activities (204)', 'Nightlife (168)', 'Shopping (163)', 'Food & Drink (135)', 'Spas & Wellness (119)', 'Nature & Parks (112)', 'Fun & Games (112)', 'Transportation (97)', 'Day Trips (71)', 'Museums (64)', 'Boat Tours & Water Sports (48)', 'Concerts & Shows (47)', 'Classes & Workshops (36)', 'See all', 'Central Business District (433)', 'Chinatown (57)', 'Southbank (41)', 'South Melbourne (27)', 'Docklands (19)', 'Lygon Street (16)', 'Chapel Street (15)', 'Port Melbourne (8)', 'Parkville (7)', 'North Melbourne (3)', 'Fitzroy (3)', 'Middle Park (1)', 'Good for Couples (270)', 'Good for a Rainy Day (270)', 'Good for Big Groups (266)', 'Budget-friendly (205)', 'Free Entry (189)', 'Good for Kids (132)', 'Honeymoon spot (66)', 'Hidden Gems (63)', 'Adventurous (37)', 'Good for Adrenaline Seekers (36)'], 'Zurich': ['Spas & Wellness (143)', 'Nightlife (110)', 'Tours (84)', 'Shopping (83)', 'Museums (67)', 'Sights & Landmarks (65)', 'Outdoor Activities (44)', 'Transportation (40)', 'Fun & Games (38)', 'Nature & Parks (27)', 'Day Trips (24)', 'Food & Drink (22)', 'Classes & Workshops (19)', 'Concerts & Shows (16)', 'Boat Tours & Water Sports (13)', 'See all', 'Good for a Rainy Day (94)', 'Free Entry (63)', 'Good for Couples (57)', 'Budget-friendly (52)', 'Good for Big Groups (48)', 'Good for Kids (44)', 'Hidden Gems (20)', 'Honeymoon spot (15)', 'Good for Adrenaline Seekers (9)', 'Adventurous (6)'], 'Oslo': ['Sights & Landmarks (163)', 'Museums (108)', 'Shopping (106)', 'Nightlife (91)', 'Outdoor Activities (74)', 'Tours (73)', 'Fun & Games (67)', 'Nature & Parks (64)', 'Spas & Wellness (34)', 'Concerts & Shows (29)', 'Boat Tours & Water Sports (21)', 'Food & Drink (17)', 'Transportation (11)', 'Classes & Workshops (11)', 'Traveler Resources (8)', 'See all', 'Good for a Rainy Day (103)', 'Good for Big Groups (85)', 'Good for Couples (84)', 'Budget-friendly (83)', 'Free Entry (81)', 'Good for Kids (71)', 'Hidden Gems (41)', 'Good for Adrenaline Seekers (21)', 'Adventurous (16)', 'Honeymoon spot (16)'], 'Helsinki': ['Shopping (133)', 'Sights & Landmarks (119)', 'Tours (109)', 'Outdoor Activities (88)', 'Museums (77)', 'Nightlife (77)', 'Fun & Games (66)', 'Nature & Parks (51)', 'Spas & Wellness (40)', 'Boat Tours & Water Sports (30)', 'Transportation (19)', 'Concerts & Shows (19)', 'Food & Drink (12)', 'Day Trips (9)', 'Traveler Resources (7)', 'See all', 'Good for a Rainy Day (138)', 'Budget-friendly (102)', 'Free Entry (96)', 'Good for Big Groups (83)', 'Good for Kids (78)', 'Good for Couples (73)', 'Hidden Gems (31)', 'Good for Adrenaline Seekers (21)', 'Honeymoon spot (17)', 'Adventurous (15)'], 'São Paulo': ['Shopping (257)', 'Sights & Landmarks (246)', 'Nightlife (246)', 'Concerts & Shows (233)', 'Museums (191)', 'Spas & Wellness (187)', 'Fun & Games (167)', 'Tours (140)', 'Outdoor Activities (107)', 'Nature & Parks (86)', 'Transportation (61)', 'Food & Drink (42)', 'Traveler Resources (33)', 'Classes & Workshops (28)', 'Boat Tours & Water Sports (17)', 'See all', 'Jardins (128)', 'Pinheiros (120)', 'Bela Vista (96)', 'Consolacao (60)', 'Republica (42)', 'Centro (38)', 'Vila Mariana (37)', 'Butanta (29)', 'Liberdade (25)', 'Vila Madalena (22)', 'Vila Buarque (21)', 'Se (18)', 'Itaim Bibi (16)', 'Higienopolis (15)', 'Ipiranga (14)', 'See all', 'Good for a Rainy Day (204)', 'Good for Kids (182)', 'Budget-friendly (170)', 'Free Entry (159)', 'Good for Big Groups (110)', 'Good for Couples (95)', 'Good for Adrenaline Seekers (37)', 'Hidden Gems (13)', 'Adventurous (8)', 'Honeymoon spot (7)'], 'Hamburg': ['Nightlife (259)', 'Tours (163)', 'Sights & Landmarks (148)', 'Shopping (101)', 'Museums (79)', 'Outdoor Activities (74)', 'Fun & Games (64)', 'Concerts & Shows (57)', 'Nature & Parks (48)', 'Spas & Wellness (36)', 'Boat Tours & Water Sports (34)', 'Food & Drink (20)', 'Classes & Workshops (13)', 'Transportation (9)', 'Traveler Resources (4)', 'See all', 'Good for a Rainy Day (114)', 'Free Entry (81)', 'Good for Big Groups (75)', 'Budget-friendly (71)', 'Good for Couples (62)', 'Good for Kids (49)', 'Honeymoon spot (23)', 'Good for Adrenaline Seekers (21)', 'Hidden Gems (17)', 'Adventurous (15)'], 'Milano': ['Sights & Landmarks (684)', 'Shopping (358)', 'Nightlife (303)', 'Tours (212)', 'Museums (191)', 'Spas & Wellness (170)', 'Food & Drink (103)', 'Fun & Games (90)', 'Nature & Parks (75)', 'Transportation (72)', 'Concerts & Shows (66)', 'Outdoor Activities (66)', 'Traveler Resources (59)', 'Classes & Workshops (41)', 'Day Trips (27)', 'See all', 'Centro Storico (886)', 'Zone 3 (199)', 'Zone 8 (137)', 'Zone 9 (130)', 'Zone 2 (126)', 'Zone 6 (125)', 'Zone 4 (107)', 'Zone 5 (85)', 'Ticinese (84)', 'Zone 7 (64)', 'Navigli (57)', 'Porta Garibaldi (56)', 'Porta Nuova (53)', "Quadrilatero della Moda (Quad d'Oro) (49)", 'Porta Venezia (47)', 'See all', 'Good for a Rainy Day (234)', 'Budget-friendly (179)', 'Good for Couples (164)', 'Free Entry (153)', 'Good for Kids (129)', 'Good for Big Groups (119)', 'Hidden Gems (57)', 'Honeymoon spot (36)', 'Good for Adrenaline Seekers (16)', 'Adventurous (11)'],{'Munich': ['Sights & Landmarks (226)', 'Tours (168)', 'Nightlife (152)', 'Shopping (105)', 'Museums (69)', 'Outdoor Activities (66)', 'Fun & Games (59)', 'Spas & Wellness (51)', 'Food & Drink (41)', 'Concerts & Shows (37)', 'Transportation (33)', 'Nature & Parks (26)', 'Day Trips (21)', 'Classes & Workshops (19)', 'Boat Tours & Water Sports (11)', 'See all', 'Good for a Rainy Day (127)', 'Good for Couples (122)', 'Budget-friendly (108)', 'Free Entry (106)', 'Good for Big Groups (103)', 'Good for Kids (81)', 'Honeymoon spot (40)', 'Good for Adrenaline Seekers (18)', 'Adventurous (16)', 'Hidden Gems (16)'], 'Buenos Aires': ['Sights & Landmarks (470)', 'Tours (418)', 'Shopping (277)', 'Nightlife (226)', 'Concerts & Shows (175)', 'Museums (163)', 'Outdoor Activities (158)', 'Spas & Wellness (152)', 'Classes & Workshops (119)', 'Fun & Games (112)', 'Transportation (94)', 'Food & Drink (92)', 'Nature & Parks (78)', 'Boat Tours & Water Sports (50)', 'Traveler Resources (15)', 'See all', 'El Centro (Downtown) (547)', 'Palermo (331)', 'San Nicolas (199)', 'Recoleta (170)', 'Microcentro (160)', 'Montserrat (138)', 'Retiro (131)', 'Theater District (109)', 'Palermo Soho (98)', 'Balvanera (84)', 'San Telmo (78)', 'Palermo Hollywood (57)', 'Belgrano (54)', 'Caballito (53)', 'Villa Crespo (49)', 'See all', 'Good for a Rainy Day (267)', 'Good for Couples (249)', 'Budget-friendly (249)', 'Good for Big Groups (200)', 'Free Entry (179)', 'Good for Kids (153)','Honeymoon spot (86)','Good for Adrenaline Seekers (50)','Hidden Gems (32)', 'Adventurous (15)']}
```


```python
dikt3={"Singapore": ["Shopping (492)", "Spas & Wellness (453)", "Sights & Landmarks (327)", "Tours (276)", "Outdoor Activities (195)", "Fun & Games (190)", "Nightlife (171)", "Museums (126)", "Transportation (124)", "Classes & Workshops (124)", "Nature & Parks (121)", "Food & Drink (116)", "Boat Tours & Water Sports (74)", "Concerts & Shows (44)", "Events (21)", "See all", "Central Area/City Area (1,038)", "Downtown Core/Downtown Singapore (288)", "Central Business District (194)", "Rochor (187)", "Orchard (182)", "Outram (179)", "Orchard Road (177)", "Chinatown (133)", "Colonial District/Civic District (106)", "Marina Bay (105)", "Boulevard (103)", "Singapore River/Riverside (102)", "Bukit Merah (94)", "Kallang (91)", "City Hall (82)", "See all", "Good for a Rainy Day (382)", "Free Entry (372)", "Budget-friendly (276)", "Good for Couples (259)", "Good for Big Groups (229)", "Good for Kids (211)", "Hidden Gems (80)", "Honeymoon spot (58)", "Good for Adrenaline Seekers (48)", "Adventurous (30)"], "Vancouver": ["Spas & Wellness (224)", "Tours (216)", "Outdoor Activities (178)", "Shopping (157)", "Sights & Landmarks (106)", "Nightlife (92)", "Food & Drink (70)", "Boat Tours & Water Sports (67)", "Museums (66)", "Nature & Parks (61)", "Fun & Games (56)", "Transportation (52)", "Concerts & Shows (51)", "Classes & Workshops (24)", "Day Trips (19)", "See all", "Central (457)", "Downtown (356)", "East Vancouver (145)", "False Creek (113)", "Fairview (113)", "Granville Street (88)", "Granville Island & Fairview (77)", "West End (76)", "Robson Street (74)", "Kitsilano (72)", "Coal Harbour (70)", "Yaletown & False Creek North (69)", "Gastown (66)", "Granville Island (59)", "Yaletown (51)", "See all", "Good for Couples (221)", "Good for a Rainy Day (186)", "Budget-friendly (156)", "Good for Big Groups (144)", "Free Entry (125)", "Good for Kids (109)", "Hidden Gems (54)", "Honeymoon spot (53)", "Good for Adrenaline Seekers (46)", "Adventurous (28)"], "London": ["Nightlife (1,223)", "Tours (1,034)", "Sights & Landmarks (977)", "Shopping (938)", "Spas & Wellness (790)", "Fun & Games (526)", "Concerts & Shows (420)", "Museums (410)", "Transportation (407)", "Outdoor Activities (298)", "Food & Drink (296)", "Classes & Workshops (293)", "Nature & Parks (257)", "Boat Tours & Water Sports (93)", "Day Trips (65)", "See all", "Soho (262)", "City of London (261)", "Mayfair (225)", "Covent Garden (211)", "Westminster (163)", "Trafalgar Square / Embankment (139)", "Marylebone (134)", "Bloomsbury (121)", "Southwark (113)", "Notting Hill (106)", "Holborn (105)", "Shoreditch (98)", "Chelsea (94)", "Fitzrovia (86)", "St. James's (84)", "See all", "Good for a Rainy Day (1,650)", "Good for Couples (1,351)", "Free Entry (1,123)", "Budget-friendly (938)", "Good for Big Groups (921)", "Good for Kids (537)", "Hidden Gems (521)", "Adventurous (175)", "Honeymoon spot (147)", "Good for Adrenaline Seekers (124)"], "Toronto": ["Spas & Wellness (334)", "Shopping (238)", "Nightlife (207)", "Tours (203)", "Fun & Games (184)", "Sights & Landmarks (181)", "Outdoor Activities (146)", "Nature & Parks (114)", "Museums (110)", "Concerts & Shows (97)", "Food & Drink (72)", "Transportation (70)", "Classes & Workshops (58)", "Boat Tours & Water Sports (47)", "Day Trips (26)", "See all", "Old Toronto (1,089)", "Downtown (639)", "Waterfront Communities-The Island (225)", "Downtown West (200)", "Midtown (167)", "West End (130)", "Entertainment District (126)", "North York (126)", "Etobicoke (116)", "East End (111)", "Church-Yonge Corridor (103)", "Bay Street Corridor (98)", "Annex (87)", "Scarborough (86)", "Kensington-Chinatown (66)", "See all", "Good for a Rainy Day (269)", "Good for Couples (269)", "Good for Big Groups (211)", "Budget-friendly (170)", "Free Entry (165)", "Good for Kids (120)", "Hidden Gems (64)", "Honeymoon spot (52)", "Good for Adrenaline Seekers (43)", "Adventurous (33)"], "Budapest": ["Tours (427)", "Sights & Landmarks (330)", "Nightlife (281)", "Shopping (263)", "Fun & Games (201)", "Outdoor Activities (150)", "Spas & Wellness (141)", "Museums (135)", "Food & Drink (131)", "Transportation (79)", "Concerts & Shows (61)", "Nature & Parks (43)", "Classes & Workshops (41)", "Boat Tours & Water Sports (37)", "Traveler Resources (7)", "See all", "District V / Inner City (297)", "District VII / Jewish Quarter (194)", "District I / Buda (147)", "Várkerület (33)", "Gellert Hill (30)", "Belváros-Lipótváros (18)", "Terézváros (13)", "Margaret Island (8)", "Erzsébetváros (7)", "Óbuda-Békásmegyer (6)", "Zugló (5)", "Kispest (5)", "Andrássy út (4)", "Városliget (4)", "Sasad (3)", "See all", "Good for a Rainy Day (335)", "Good for Couples (330)", "Budget-friendly (313)", "Good for Big Groups (281)", "Free Entry (183)", "Good for Kids (171)", "Hidden Gems (124)", "Honeymoon spot (95)", "Good for Adrenaline Seekers (70)", "Adventurous (47)"], "Hong Kong": ["Shopping (485)", "Sights & Landmarks (350)", "Tours (251)", "Outdoor Activities (195)", "Nature & Parks (174)", "Spas & Wellness (145)", "Museums (112)", "Fun & Games (100)", "Nightlife (96)", "Food & Drink (91)", "Classes & Workshops (69)", "Boat Tours & Water Sports (67)", "Transportation (48)", "Concerts & Shows (23)", "Events (18)", "See all", "Hong Kong Island (436)", "Kowloon (242)", "New Territories (232)", "Central District (224)", "Yau Tsim Mong District (171)", "Central (135)", "Tsim Sha Tsui (95)", "Southern District (50)", "Islands District (50)", "Sheung Wan (49)", "Mong Kok (39)", "Eastern District (36)", "Sai Kung (35)", "Yuen Long (34)", "Sha Tin (34)", "See all", "Free Entry (381)", "Budget-friendly (257)", "Good for a Rainy Day (252)", "Good for Couples (234)", "Good for Kids (203)", "Good for Big Groups (134)", "Hidden Gems (57)", "Honeymoon spot (40)", "Good for Adrenaline Seekers (22)", "Adventurous (14)"], "Stockholm": ["Tours (140)", "Sights & Landmarks (119)", "Outdoor Activities (101)", "Shopping (86)", "Museums (77)", "Fun & Games (64)", "Nature & Parks (60)", "Boat Tours & Water Sports (50)", "Nightlife (40)", "Spas & Wellness (39)", "Concerts & Shows (28)", "Transportation (21)", "Food & Drink (21)", "Classes & Workshops (10)", "Traveler Resources (9)", "See all", "Norrmalm (120)", "Sodermalm Borough (87)", "Sodermalm (82)", "Gamla Stan & Riddarholmen (80)", "Ostermalm (78)", "Kungsholmen (32)", "Vasastan (32)", "Djurgarden & Djurgardsbrunn (32)", "SoFo & Medborgarplatsen (25)", "Enskede-Arsta-Vantor Borough (20)", "Mariatorget (16)", "Hornstull & Langholmen (13)", "Johanneshov (10)", "Slussen (10)", "Skeppsholmen (8)", "See all", "Good for a Rainy Day (141)", "Budget-friendly (127)", "Good for Couples (114)", "Good for Kids (82)", "Free Entry (80)", "Good for Big Groups (79)", "Hidden Gems (36)", "Honeymoon spot (30)", "Good for Adrenaline Seekers (17)", "Adventurous (16)"], "Sydney": ["Tours (510)", "Outdoor Activities (336)", "Spas & Wellness (282)", "Nightlife (218)", "Shopping (214)", "Sights & Landmarks (187)", "Boat Tours & Water Sports (152)", "Nature & Parks (143)", "Food & Drink (130)", "Fun & Games (128)", "Transportation (110)", "Museums (99)", "Concerts & Shows (57)", "Classes & Workshops (57)", "Day Trips (37)", "See all", "Central Business District (367)", "The Rocks (81)", "Surry Hills (60)", "Darlinghurst (53)", "Paddington (46)", "Darling Harbour (44)", "Newtown (43)", "Balmain (30)", "Double Bay (26)", "Chinatown (21)", "Glebe (18)", "Inner West (12)", "Inner East (11)", "Manly (10)", "Mosman (10)", "See all", "Good for Big Groups (348)", "Good for Couples (334)", "Good for a Rainy Day (277)", "Budget-friendly (274)", "Free Entry (255)", "Good for Kids (187)", "Honeymoon spot (90)", "Hidden Gems (87)", "Good for Adrenaline Seekers (74)", "Adventurous (64)"], "Kuala Lumpur": ["Tours (193)", "Shopping (155)", "Spas & Wellness (147)", "Transportation (137)", "Sights & Landmarks (106)", "Outdoor Activities (95)", "Nightlife (93)", "Day Trips (76)", "Fun & Games (65)", "Museums (53)", "Food & Drink (47)", "Classes & Workshops (46)", "Nature & Parks (35)", "Concerts & Shows (18)", "Boat Tours & Water Sports (14)", "See all", "Good for a Rainy Day (188)", "Free Entry (154)", "Budget-friendly (150)", "Good for Couples (149)", "Good for Big Groups (130)", "Good for Kids (119)", "Hidden Gems (29)", "Honeymoon spot (26)", "Good for Adrenaline Seekers (24)", "Adventurous (14)"], "Barcelona": ["Tours (823)", "Nightlife (594)", "Spas & Wellness (560)", "Sights & Landmarks (511)", "Outdoor Activities (443)", "Shopping (426)", "Food & Drink (256)", "Fun & Games (210)", "Museums (165)", "Classes & Workshops (150)", "Boat Tours & Water Sports (126)", "Transportation (118)", "Concerts & Shows (116)", "Nature & Parks (115)", "Day Trips (63)", "See all", "Ciutat Vella (Old Town) (956)", "Eixample (742)", "Barrio Gotico (Barri Gotic) (419)", "La Dreta de l'Eixample (315)", "Sant Marti (265)", "Sant Pere, Santa Caterina i la Ribera (248)", "El Born / La Ribera (222)", "El Raval (211)", "Gracia (197)", "L"Antiga Esquerra de l"Eixample (167)", "Vila de Gracia (144)", "Ciutadella / Vila Olimpica (138)", "Sant Gervasi-Galvany (103)", "La Rambla (102)", "Les Corts (94)", "See all", "Good for Couples (503)", "Good for a Rainy Day (466)", "Budget-friendly (450)", "Good for Big Groups (358)", "Good for Kids (271)", "Free Entry (241)", "Hidden Gems (201)", "Honeymoon spot (201)", "Good for Adrenaline Seekers (129)", "Adventurous (54)"], "Paris": ["Sights & Landmarks (1,880)", "Spas & Wellness (932)", "Shopping (842)", "Tours (834)", "Nightlife (497)", "Museums (281)", "Transportation (275)", "Concerts & Shows (270)", "Fun & Games (262)", "Food & Drink (251)", "Nature & Parks (242)", "Outdoor Activities (222)", "Classes & Workshops (218)", "Day Trips (63)", "Traveler Resources (60)", "See all", "Opera / Bourse (502)", "1st Arr. - Louvre (377)", "8th Arr. - Elysee (373)", "6th Arr. - Luxembourg (345)", "Le Marais (341)", "16th Arr. - Passy (317)", "9th Arr. - Opera (308)", "4th Arr. - Hotel-de-Ville (300)" ]}    
```


      File "<ipython-input-9-c9b52c23f0c5>", line 1
        dikt3={"Singapore": ["Shopping (492)", "Spas & Wellness (453)", "Sights & Landmarks (327)", "Tours (276)", "Outdoor Activities (195)", "Fun & Games (190)", "Nightlife (171)", "Museums (126)", "Transportation (124)", "Classes & Workshops (124)", "Nature & Parks (121)", "Food & Drink (116)", "Boat Tours & Water Sports (74)", "Concerts & Shows (44)", "Events (21)", "See all", "Central Area/City Area (1,038)", "Downtown Core/Downtown Singapore (288)", "Central Business District (194)", "Rochor (187)", "Orchard (182)", "Outram (179)", "Orchard Road (177)", "Chinatown (133)", "Colonial District/Civic District (106)", "Marina Bay (105)", "Boulevard (103)", "Singapore River/Riverside (102)", "Bukit Merah (94)", "Kallang (91)", "City Hall (82)", "See all", "Good for a Rainy Day (382)", "Free Entry (372)", "Budget-friendly (276)", "Good for Couples (259)", "Good for Big Groups (229)", "Good for Kids (211)", "Hidden Gems (80)", "Honeymoon spot (58)", "Good for Adrenaline Seekers (48)", "Adventurous (30)"], "Vancouver": ["Spas & Wellness (224)", "Tours (216)", "Outdoor Activities (178)", "Shopping (157)", "Sights & Landmarks (106)", "Nightlife (92)", "Food & Drink (70)", "Boat Tours & Water Sports (67)", "Museums (66)", "Nature & Parks (61)", "Fun & Games (56)", "Transportation (52)", "Concerts & Shows (51)", "Classes & Workshops (24)", "Day Trips (19)", "See all", "Central (457)", "Downtown (356)", "East Vancouver (145)", "False Creek (113)", "Fairview (113)", "Granville Street (88)", "Granville Island & Fairview (77)", "West End (76)", "Robson Street (74)", "Kitsilano (72)", "Coal Harbour (70)", "Yaletown & False Creek North (69)", "Gastown (66)", "Granville Island (59)", "Yaletown (51)", "See all", "Good for Couples (221)", "Good for a Rainy Day (186)", "Budget-friendly (156)", "Good for Big Groups (144)", "Free Entry (125)", "Good for Kids (109)", "Hidden Gems (54)", "Honeymoon spot (53)", "Good for Adrenaline Seekers (46)", "Adventurous (28)"], "London": ["Nightlife (1,223)", "Tours (1,034)", "Sights & Landmarks (977)", "Shopping (938)", "Spas & Wellness (790)", "Fun & Games (526)", "Concerts & Shows (420)", "Museums (410)", "Transportation (407)", "Outdoor Activities (298)", "Food & Drink (296)", "Classes & Workshops (293)", "Nature & Parks (257)", "Boat Tours & Water Sports (93)", "Day Trips (65)", "See all", "Soho (262)", "City of London (261)", "Mayfair (225)", "Covent Garden (211)", "Westminster (163)", "Trafalgar Square / Embankment (139)", "Marylebone (134)", "Bloomsbury (121)", "Southwark (113)", "Notting Hill (106)", "Holborn (105)", "Shoreditch (98)", "Chelsea (94)", "Fitzrovia (86)", "St. James's (84)", "See all", "Good for a Rainy Day (1,650)", "Good for Couples (1,351)", "Free Entry (1,123)", "Budget-friendly (938)", "Good for Big Groups (921)", "Good for Kids (537)", "Hidden Gems (521)", "Adventurous (175)", "Honeymoon spot (147)", "Good for Adrenaline Seekers (124)"], "Toronto": ["Spas & Wellness (334)", "Shopping (238)", "Nightlife (207)", "Tours (203)", "Fun & Games (184)", "Sights & Landmarks (181)", "Outdoor Activities (146)", "Nature & Parks (114)", "Museums (110)", "Concerts & Shows (97)", "Food & Drink (72)", "Transportation (70)", "Classes & Workshops (58)", "Boat Tours & Water Sports (47)", "Day Trips (26)", "See all", "Old Toronto (1,089)", "Downtown (639)", "Waterfront Communities-The Island (225)", "Downtown West (200)", "Midtown (167)", "West End (130)", "Entertainment District (126)", "North York (126)", "Etobicoke (116)", "East End (111)", "Church-Yonge Corridor (103)", "Bay Street Corridor (98)", "Annex (87)", "Scarborough (86)", "Kensington-Chinatown (66)", "See all", "Good for a Rainy Day (269)", "Good for Couples (269)", "Good for Big Groups (211)", "Budget-friendly (170)", "Free Entry (165)", "Good for Kids (120)", "Hidden Gems (64)", "Honeymoon spot (52)", "Good for Adrenaline Seekers (43)", "Adventurous (33)"], "Budapest": ["Tours (427)", "Sights & Landmarks (330)", "Nightlife (281)", "Shopping (263)", "Fun & Games (201)", "Outdoor Activities (150)", "Spas & Wellness (141)", "Museums (135)", "Food & Drink (131)", "Transportation (79)", "Concerts & Shows (61)", "Nature & Parks (43)", "Classes & Workshops (41)", "Boat Tours & Water Sports (37)", "Traveler Resources (7)", "See all", "District V / Inner City (297)", "District VII / Jewish Quarter (194)", "District I / Buda (147)", "Várkerület (33)", "Gellert Hill (30)", "Belváros-Lipótváros (18)", "Terézváros (13)", "Margaret Island (8)", "Erzsébetváros (7)", "Óbuda-Békásmegyer (6)", "Zugló (5)", "Kispest (5)", "Andrássy út (4)", "Városliget (4)", "Sasad (3)", "See all", "Good for a Rainy Day (335)", "Good for Couples (330)", "Budget-friendly (313)", "Good for Big Groups (281)", "Free Entry (183)", "Good for Kids (171)", "Hidden Gems (124)", "Honeymoon spot (95)", "Good for Adrenaline Seekers (70)", "Adventurous (47)"], "Hong Kong": ["Shopping (485)", "Sights & Landmarks (350)", "Tours (251)", "Outdoor Activities (195)", "Nature & Parks (174)", "Spas & Wellness (145)", "Museums (112)", "Fun & Games (100)", "Nightlife (96)", "Food & Drink (91)", "Classes & Workshops (69)", "Boat Tours & Water Sports (67)", "Transportation (48)", "Concerts & Shows (23)", "Events (18)", "See all", "Hong Kong Island (436)", "Kowloon (242)", "New Territories (232)", "Central District (224)", "Yau Tsim Mong District (171)", "Central (135)", "Tsim Sha Tsui (95)", "Southern District (50)", "Islands District (50)", "Sheung Wan (49)", "Mong Kok (39)", "Eastern District (36)", "Sai Kung (35)", "Yuen Long (34)", "Sha Tin (34)", "See all", "Free Entry (381)", "Budget-friendly (257)", "Good for a Rainy Day (252)", "Good for Couples (234)", "Good for Kids (203)", "Good for Big Groups (134)", "Hidden Gems (57)", "Honeymoon spot (40)", "Good for Adrenaline Seekers (22)", "Adventurous (14)"], "Stockholm": ["Tours (140)", "Sights & Landmarks (119)", "Outdoor Activities (101)", "Shopping (86)", "Museums (77)", "Fun & Games (64)", "Nature & Parks (60)", "Boat Tours & Water Sports (50)", "Nightlife (40)", "Spas & Wellness (39)", "Concerts & Shows (28)", "Transportation (21)", "Food & Drink (21)", "Classes & Workshops (10)", "Traveler Resources (9)", "See all", "Norrmalm (120)", "Sodermalm Borough (87)", "Sodermalm (82)", "Gamla Stan & Riddarholmen (80)", "Ostermalm (78)", "Kungsholmen (32)", "Vasastan (32)", "Djurgarden & Djurgardsbrunn (32)", "SoFo & Medborgarplatsen (25)", "Enskede-Arsta-Vantor Borough (20)", "Mariatorget (16)", "Hornstull & Langholmen (13)", "Johanneshov (10)", "Slussen (10)", "Skeppsholmen (8)", "See all", "Good for a Rainy Day (141)", "Budget-friendly (127)", "Good for Couples (114)", "Good for Kids (82)", "Free Entry (80)", "Good for Big Groups (79)", "Hidden Gems (36)", "Honeymoon spot (30)", "Good for Adrenaline Seekers (17)", "Adventurous (16)"], "Sydney": ["Tours (510)", "Outdoor Activities (336)", "Spas & Wellness (282)", "Nightlife (218)", "Shopping (214)", "Sights & Landmarks (187)", "Boat Tours & Water Sports (152)", "Nature & Parks (143)", "Food & Drink (130)", "Fun & Games (128)", "Transportation (110)", "Museums (99)", "Concerts & Shows (57)", "Classes & Workshops (57)", "Day Trips (37)", "See all", "Central Business District (367)", "The Rocks (81)", "Surry Hills (60)", "Darlinghurst (53)", "Paddington (46)", "Darling Harbour (44)", "Newtown (43)", "Balmain (30)", "Double Bay (26)", "Chinatown (21)", "Glebe (18)", "Inner West (12)", "Inner East (11)", "Manly (10)", "Mosman (10)", "See all", "Good for Big Groups (348)", "Good for Couples (334)", "Good for a Rainy Day (277)", "Budget-friendly (274)", "Free Entry (255)", "Good for Kids (187)", "Honeymoon spot (90)", "Hidden Gems (87)", "Good for Adrenaline Seekers (74)", "Adventurous (64)"], "Kuala Lumpur": ["Tours (193)", "Shopping (155)", "Spas & Wellness (147)", "Transportation (137)", "Sights & Landmarks (106)", "Outdoor Activities (95)", "Nightlife (93)", "Day Trips (76)", "Fun & Games (65)", "Museums (53)", "Food & Drink (47)", "Classes & Workshops (46)", "Nature & Parks (35)", "Concerts & Shows (18)", "Boat Tours & Water Sports (14)", "See all", "Good for a Rainy Day (188)", "Free Entry (154)", "Budget-friendly (150)", "Good for Couples (149)", "Good for Big Groups (130)", "Good for Kids (119)", "Hidden Gems (29)", "Honeymoon spot (26)", "Good for Adrenaline Seekers (24)", "Adventurous (14)"], "Barcelona": ["Tours (823)", "Nightlife (594)", "Spas & Wellness (560)", "Sights & Landmarks (511)", "Outdoor Activities (443)", "Shopping (426)", "Food & Drink (256)", "Fun & Games (210)", "Museums (165)", "Classes & Workshops (150)", "Boat Tours & Water Sports (126)", "Transportation (118)", "Concerts & Shows (116)", "Nature & Parks (115)", "Day Trips (63)", "See all", "Ciutat Vella (Old Town) (956)", "Eixample (742)", "Barrio Gotico (Barri Gotic) (419)", "La Dreta de l'Eixample (315)", "Sant Marti (265)", "Sant Pere, Santa Caterina i la Ribera (248)", "El Born / La Ribera (222)", "El Raval (211)", "Gracia (197)", "L"Antiga Esquerra de l"Eixample (167)", "Vila de Gracia (144)", "Ciutadella / Vila Olimpica (138)", "Sant Gervasi-Galvany (103)", "La Rambla (102)", "Les Corts (94)", "See all", "Good for Couples (503)", "Good for a Rainy Day (466)", "Budget-friendly (450)", "Good for Big Groups (358)", "Good for Kids (271)", "Free Entry (241)", "Hidden Gems (201)", "Honeymoon spot (201)", "Good for Adrenaline Seekers (129)", "Adventurous (54)"], "Paris": ["Sights & Landmarks (1,880)", "Spas & Wellness (932)", "Shopping (842)", "Tours (834)", "Nightlife (497)", "Museums (281)", "Transportation (275)", "Concerts & Shows (270)", "Fun & Games (262)", "Food & Drink (251)", "Nature & Parks (242)", "Outdoor Activities (222)", "Classes & Workshops (218)", "Day Trips (63)", "Traveler Resources (60)", "See all", "Opera / Bourse (502)", "1st Arr. - Louvre (377)", "8th Arr. - Elysee (373)", "6th Arr. - Luxembourg (345)", "Le Marais (341)", "16th Arr. - Passy (317)", "9th Arr. - Opera (308)", "4th Arr. - Hotel-de-Ville (300)" ]}
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           ^
    SyntaxError: invalid syntax
    



```python

```


      File "<ipython-input-3-d9fb13493b9e>", line 1
        jupyter nbconvert --to html Tripadvisor-Number_Thingstodo.ipynb
                        ^
    SyntaxError: invalid syntax
    



```python

```
