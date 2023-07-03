# Arduino-RFID-Door-Locks
The purpose of this project is to replace a hotel's room door locks with electromagnetic ones that are controlled by a microcontroller (Arduino UNO). 

Modules used:
  1) Arduino UNO
  2) Mifare RC522 RFID Card Reader (13.56MHz field)
  3) DS3231 Real Time Clock Module
  4) SD Card Reader Module
     
First of all a Master Card has to be set. The Master Card is used when a card is needed to be in the "blacklist" of a specific door. This can be done in cases
such as when a specific card is lost. Then the owner can make a clone of this card (using its UID) and pass it above the rfid reader of this door after the Master Card
has passed. Then this door won't accept any card with this UID, even if it's valid. This blacklist is stored in Arduino's EEPROM.

This project was made for hotel usage and consists of 3 parts:
  1) Owner Arduino / Mifare Cards encryption: 
      Before anything else the cards have to be encrypted so that only the owner can read and edit them. Both key A and key B of the mifare
      card is changed using this code. Every other script from now on authenticates the card using our own encryption keys.
      Note: The Master Card doesn't have to be encrypted.   
  3) Reception Arduino / Mifare Cards preparation: 
      The receptionist inputs First Name and Last Name of the customer, the Room Number of the Room they are about to stay and the 
      Date of Departure (the door automatically declines every expired card). All this info is stored in the (64bits) memory of the card.
  4) Door Arduino / Mifare Card Validation: 
      Every room has an electromagnetic door lock that is controlled by an Arduino UNO, which is programmed to check the validity of a card.
      Besides checking the Room Number and Date of Departure, secret codes has also been created and implemented for even greater protection.
      There is also functionality for passpartout cards, given to the hotel stuff.
     

There are also 4 help scripts:
1) A script to set up the clock of every RTC module.
2) A script to prepare the EEPROM of every Arduino UNO. This is done for easier searching the EEPROM for blacklisted cards.
3) A script to set up a Master Card.
