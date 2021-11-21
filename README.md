1) kui konveieri andurilt signaale ei tule, siis lülitada välja söötja ja ahi. Normaalses olukorras 2 sekundi jooksul 1 piuks.
2) kui õhuandur registreerib temperatuuri alla 40 kraadi, siis lülitab välja ventilaatorid.
3) kui temperatuuriandur registreerib ülekuumuse, siis lülitab välja ahju.
4) Kui ventilaatori häire, siis lülitada välja ahi.
5) Kui söötja võll jääb seisma, siis lülitada välja ahi. Ületemp/Alatemp


PLC paneelilt peaks siis saama kasutaja teha järgmist:
1) ALARM RESET;
2) seadistada etteantud temperatuuri (ülemist), mille juures ahi tuleb lülitada välja.
Alarm käivitub kui tekib mingi häire:
  (konveieri võll jääb seisma,
   söötja võll jääb seisma,
   ventilaatori kaitsmed rakenduvad,
   ülekuumus,
   toitepinge häire,
   alatemperatuur)
Kõidel juhtudel tuleb seda ka kuvada rasvaselt ekraanil ja käivitada alarm.
Samuti tuleb kõikidel nendel juhtudel saata SMS mingile kindlale numbrile.


Sisse-väljalülitamine
---------------------
Rubilnikuga


Konfigureeritavad suurused
--------------------------
1. ALATEMP = Alatemperatuur = Ventilaatorite väljalülitamise temperatuur
2. VENT_ON_TEMP = Ventilaatorite sisselülitamise temperatuur
3. YLETEMP = Ülekuumenemise temperatuur


Abimuutujad
-----------
KONVEIER_TÖÖTAB = Konveierilt on viimase 2 sekundi jooksul mingi impulss tulnud.
ALARM_KONVEIER
ALARM_SOOTJA
ALARM_VENTILAATOR = VENTILAATOR1_ALARM OR VENTILAATOR2_ALARM
ALARM_YLETEMPERATUUR
ALARM_ALATEMPERATUUR
ALARM_TOIDE


Väljundite juhtimine
--------------------
AHI = NOT (ALARM_KONVEIER OR ALARM_SOOTJA OR ALARM_VENTILAATOR OR ALARM_YLETEMPERATUUR)
VENTILAATOR =
   AHI
   	OR
   R/S TRIGGER
   	SET = TEMP > VENT_ON_TEMP
   	RESET = TEMP < ALATEMP

SÖöTJA START = KONVEIER_TöÖTAB

SIGNALISATSIOON = ükspuha mis ALARM

SMS = ükspuha mis ALARM; v.a. ALARM_ALATEMPERATUUR
