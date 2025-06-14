# codetech-task-4

COMPANY : CODETECH IT SOLUTIONS

NAME : KODELA KALYANI

INTERN ID : CTO4D41753

DOMAIN : EMBEDDED SYSTEMS

DURATION : 4 WEEKS

MENTOR : NEELA SANTHOSH

DESCRIPTION : 6SHHFKUHFRJQLWLRQV\VWHPVKDYHDQRWKHUFRQVWUDLQWFRQFHUQLQJWKHVW\OHRIVSHHFKWKH\FDQUHFRJQL]H
7KH\DUHWKUHHVW\OHVRIVSHHFKLVRODWHGFRQQHFWHGDQGFRQWLQXRXV
A. Isolated
7KLV VSHHFK UHFRJQLWLRQ V\VWHPFDQMXVW KDQGOHZRUGVWKDW DUH VSRNHQ VHSDUDWHO\ 7KLVLVWKHPRVWFRPPRQ
VSHHFKUHFRJQLWLRQV\VWHPVDYDLODEOHWRGD\7KHXVHUPXVWSDXVHEHWZHHQHDFKZRUGDQGFRPPDQGVSRNHQ7KH
VSHHFKUHFRJQLWLRQFLUFXLWLVVHWXSWRLGHQWLI\LVRODWHGZRUGVRIVHFRQGOHQJWKV,VRODWHGZRUGUHFRJQL]HUV
XVXDOO\UHTXLUHHDFKXWWHUDQFHWRKDYHTXLHWODFNRIDQDXGLRVLJQDORQ%27+VLGHVRIWKHVDPSOHZLQGRZ,W
GRHVQ
WPHDQWKDWLWDFFHSWVVLQJOHZRUGVEXWGRHVUHTXLUHDVLQJOHXWWHUDQFHDWDWLPH2IWHQWKHVHV\VWHPVKDYH
/LVWHQ1RW/LVWHQVWDWHVZKHUHWKH\UHTXLUHWKHVSHDNHUWRZDLWEHWZHHQXWWHUDQFHVXVXDOO\GRLQJSURFHVVLQJ
GXULQJWKHSDXVHV,VRODWHG8WWHUDQFHPLJKWEHDEHWWHUQDPHIRUWKLVFODVV>@
B. Connected
&RQQHFWZRUGV\VWHPVRUPRUHFRUUHFWO\
FRQQHFWHGXWWHUDQFHV
DUHVLPLODUWR,VRODWHGZRUGVEXWDOORZVHSDUDWH
XWWHUDQFHVWREH
UXQWRJHWKHU
ZLWKDPLQLPDOSDXVHEHWZHHQWKHP,WLVDKDOIZD\SRLQWEHWZHHQLVRODWHGZRUG
DQGFRQWLQXRXVVSHHFKUHFRJQLWLRQ
C. Continuous
&RQWLQXRXVUHFRJQLWLRQLVWKHQH[WVWHS5HFRJQL]HUVZLWKFRQWLQXRXVVSHHFKFDSDELOLWLHVDUHVRPHRIWKHPRVW
GLIILFXOWWRFUHDWHEHFDXVHWKH\PXVWXWLOL]HVSHFLDOPHWKRGVWRGHWHUPLQHXWWHUDQFHERXQGDULHV&RQWLQXRXVVSHHFK
UHFRJQL]HUV DOORZ XVHUV WR VSHDN DOPRVW QDWXUDOO\ ZKLOH WKH FRPSXWHU GHWHUPLQHV WKH FRQWHQW %DVLFDOO\ LW
FRPSXWHUGLFWDWLRQ ,WLVWKHQDWXUDOFRQYHUVDWLRQDOVSHHFKZHDUHXVHWRLQHYHU\GD\OLIH,WLV H[WUHPHO\GLIILFXOW
IRUD UHFRJQL]HUWRVKLIWWKURXJKWKHWH[WDVWKHZRUGWHQGVWRPHUJHWRJHWKHU)RULQVWDQFH+LKRZDUH\RX
GRLQJ"VRXQGVOLNH+LKRZ\DGRLQ&RQWLQXRXVVSHHFKUHFRJQLWLRQV\VWHPVDUHRQWKHPDUNHWDQGDUHXQGHU
FRQWLQXDOGHYHORSPHQW

SYSTEM DESIGN : 

 <img width="247" alt="image" src="https://github.com/user-attachments/assets/4bcae367-9c25-43c3-8c14-a025a471f9b6" />

 CODE : 

 // Callback function for VR engine
void VRCallback(int nFlag, int nID, int nScore, int nSG, int nEnergy)
{
  if (nFlag==DSpotterSDKHL::InitSuccess)
  {
      //ToDo
  }
  else if (nFlag==DSpotterSDKHL::GetResult)
  {
      /*
      When getting an recognition result,
      the following index and scores are also return to the VRCallback function:
          nID        The result command id
          nScore     nScore is used to evaluate how good or bad the result is.
                     The higher the score, the more similar the voice and the result command are.
          nSG        nSG is the gap between the voice and non-command (Silence/Garbage) models.
                     The higher the score, the less similar the voice and non-command (Silence/Garbage) models are.
          nEnergy    nEnergy is the voice energy level.
                     The higher the score, the louder the voice.
      */
      //ToDo
      switch(nID)
      {
          case 100:
            Serial.println("The Trigger was heard");
            // Add your own code here
            break;
          case 10000:
            Serial.println("The Command -read- was heard");
            // Add your own code here
            break;
          case 10001:
            Serial.println("The Command -upload- was heard");
            // Add your own code here
            break;
          case 10002:
            Serial.println("The Command -share- was heard");
            // Add your own code here
            break;
          default:
            break;
      }

  }
  else if (nFlag==DSpotterSDKHL::ChangeStage)
  {
      switch(nID)
      {
          case DSpotterSDKHL::TriggerStage:
            LED_RGB_Off();
            LED_BUILTIN_Off();
            break;
          case DSpotterSDKHL::CommandStage:
            LED_BUILTIN_On();
            break;
          default:
            break;
      }
  }
  else if (nFlag==DSpotterSDKHL::GetError)
  {
      if (nID == DSpotterSDKHL::LicenseFailed)
      {
          //Serial.print("DSpotter license failed! The serial number of your device is ");
          //Serial.println(DSpotterSDKHL::GetSerialNumber());
      }
      g_oDSpotterSDKHL.Release();
      while(1);//hang loop
  }
  else if (nFlag == DSpotterSDKHL::LostRecordFrame)
  {
      //ToDo
  }
}

OUTPUT :

![image](https://github.com/user-attachments/assets/902482da-7870-40b4-a2c5-558538071b13)

WORKING DEMO : 

https://youtu.be/fRSVQ4Fkwjc?si=QLlAV47lBe3NE9zf








