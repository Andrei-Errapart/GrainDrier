1) kui konveieri andurilt signaale ei tule, siis l�litada v�lja s��tja ja ahi. Normaalses olukorras 2 sekundi jooksul 1 piuks.
2) kui �huandur registreerib temperatuuri alla 40 kraadi, siis l�litab v�lja ventilaatorid.
3) kui temperatuuriandur registreerib �lekuumuse, siis l�litab v�lja ahju.
4) Kui ventilaatori h�ire, siis l�litada v�lja ahi.
5) Kui s��tja v�ll j��b seisma, siis l�litada v�lja ahi. �letemp/Alatemp


PLC paneelilt peaks siis saama kasutaja teha j�rgmist:
1) ALARM RESET;
2) seadistada etteantud temperatuuri (�lemist), mille juures ahi tuleb l�litada v�lja.
Alarm k�ivitub kui tekib mingi h�ire:
  (konveieri v�ll j��b seisma,
   s��tja v�ll j��b seisma,
   ventilaatori kaitsmed rakenduvad,
   �lekuumus,
   toitepinge h�ire,
   alatemperatuur)
K�idel juhtudel tuleb seda ka kuvada rasvaselt ekraanil ja k�ivitada alarm.
Samuti tuleb k�ikidel nendel juhtudel saata SMS mingile kindlale numbrile.


Sisse-v�ljal�litamine
---------------------
Rubilnikuga


Konfigureeritavad suurused
--------------------------
1. ALATEMP = Alatemperatuur = Ventilaatorite v�ljal�litamise temperatuur
2. VENT_ON_TEMP = Ventilaatorite sissel�litamise temperatuur
3. YLETEMP = �lekuumenemise temperatuur


Abimuutujad
-----------
KONVEIER_T��TAB = Konveierilt on viimase 2 sekundi jooksul mingi impulss tulnud.
ALARM_KONVEIER
ALARM_SOOTJA
ALARM_VENTILAATOR = VENTILAATOR1_ALARM OR VENTILAATOR2_ALARM
ALARM_YLETEMPERATUUR
ALARM_ALATEMPERATUUR
ALARM_TOIDE


V�ljundite juhtimine
--------------------
AHI = NOT (ALARM_KONVEIER OR ALARM_SOOTJA OR ALARM_VENTILAATOR OR ALARM_YLETEMPERATUUR)
VENTILAATOR =
   AHI
   	OR
   R/S TRIGGER
   	SET = TEMP > VENT_ON_TEMP
   	RESET = TEMP < ALATEMP

S��TJA START = KONVEIER_T��TAB

SIGNALISATSIOON = �kspuha mis ALARM

SMS = �kspuha mis ALARM; v.a. ALARM_ALATEMPERATUUR
