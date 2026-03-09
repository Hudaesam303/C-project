#include<stdio.h>
#include<Stdlib.h>
#define WITH_ENGINE_TEMP_CONTROLLER 0 //define WITH_ENGINE_TEMP_CONTROLLER as 1 to enable engine temperature controller
// N is Defined as ON ... F is Defined as OFF
typedef enum //define the vehicle system
{
	TurnONTheVehicle='a',
	TurnOFFTheVehicle='b',
	QuiteTheSystem='c'
}System;
typedef enum //define the sensor types
{

	Turnofftheengine='a',
	Setthetrafficlightcolor='b',
	Settheroomtemperature='c',
	Settheenginetemperature='d'
}Sensor;
typedef enum //define the traffic lights colors
{
	green='G',
	red='R',
	orange='O'

}TrafficColors;
typedef enum //give a constant values fot all Tempretures
{
	HighRoomTEMP=40,
	LowRoomTEMP=10,
	HighEngineTEMP=150,
	LowEngineTEMP=100

}Tempretures;
typedef enum
{
	speedHIGH=100,
	speedLow=30,
	speedZERO=0

}Speeds;
typedef enum //set default values foe temps
{
	defaultROOMTEMP=20,
	defaultENGINETEMPS=125

}DefaultTEMPS;
struct Data //define the data which should appear every time when the system on
{
	char Engine; //ON OR OFF
	char AC; //ON OR OFF
	int vehicleSpeed; //IN KM\H
	int RoomTempreture;  //IN CELSUIS
	char EngTempController; //ON OR OFF
	int EngineTemp; //IN CELSUIS

}vehicle;
// Declare global variables
struct Data Vehicle; // the vehicle object
char input; // the user input
char traffic_light; // the traffic light color


// Declare helper functions
void print_menu(); // print the main menu
void print_sensors_menu(); // print the sensors menu
void print_vehicle_state(); // print the current vehicle state
void update_vehicle_state(); // update the vehicle state based on user input and sensor readings
void get_input(); // get a character input from the user

int main()
{
	setvbuf(stdout, NULL, _IONBF, 0);
	//intilaize the vehicle massage at first
	vehicle.Engine='F';
	vehicle.AC='F';
	vehicle.vehicleSpeed=speedZERO;
	vehicle.RoomTempreture=defaultROOMTEMP;
	vehicle.EngineTemp=defaultENGINETEMPS;
	vehicle.EngTempController='F';

	while(1)
	{
        print_menu();
		get_input();


if(input==QuiteTheSystem) //the last choice in the system
	{
		setvbuf(stdout, NULL, _IONBF, 0);
		printf("TRY TO RUN THE SYSTEM AGAIN , THAMK YOU. \n \n");
		break;//to go out from the system
	}
	else if(input==TurnOFFTheVehicle)//if the user chose to turn off the vehicle the engine will be off
	{
		setvbuf(stdout, NULL, _IONBF, 0);
		vehicle.Engine='F';
		printf("The Engine is Turned OFF. \n \n");
		print_menu();

	}
	 if(input==TurnONTheVehicle) //if the user chose to turn on the vehicle the engine will be on
		{
		setvbuf(stdout, NULL, _IONBF, 0);
			vehicle.Engine='N';
			//printf("The Engine is Turned ON. \n \n");
			//print_sensors_menu();///////////////////////////////////////
		}


	else
	{
		setvbuf(stdout, NULL, _IONBF, 0);
		printf("Invalid Data ... \n \n");
		continue;
	}
	//continue;

	if(vehicle.Engine == 'N')///////
	{
		// Print the sensors menu
		 print_sensors_menu();

		 // Get the user input
		   get_input();
		   if(input==Turnofftheengine)
		   {
			   setvbuf(stdout, NULL, _IONBF, 0);
			   printf("TRY TO RUN THE SYSTEM AGAIN , THAMK YOU. \n");
			   		break;//to go out from the system
		   }
		   else if(input==Setthetrafficlightcolor)
		   {
		       //scanf(" %c",&traffic_light);
		       update_vehicle_state();
			   setvbuf(stdout, NULL, _IONBF, 0);
			   printf("Enter The Traffic Color (G,O,R) : \n ");
			   scanf(" %c",&traffic_light);
			   update_vehicle_state();
			   printf("The traffic light color is set to %c.\n\n", traffic_light);
			   print_vehicle_state();

		   }
		   else if(input==Settheroomtemperature)
		   {setvbuf(stdout, NULL, _IONBF, 0);
		         printf("Enter the room temperature (°C): ");
		         scanf("%d", &vehicle.RoomTempreture);
		         update_vehicle_state();
		         printf("The room temperature is set to %d °C.\n\n", vehicle.RoomTempreture);
		         print_vehicle_state();


		   }
		   else if(input==Settheenginetemperature)
		   {
			   setvbuf(stdout, NULL, _IONBF, 0);
			   printf("Enter the Engine temperature (°C): ");
			   scanf("%d", &vehicle.EngineTemp);
			   update_vehicle_state();
			    printf("The room temperature is set to %d °C.\n\n", vehicle.EngineTemp);
			     print_vehicle_state();
		   }
		   else
		   {
		      // Invalid input
		       printf("Invalid input. Please try again.\n\n");
		        continue;
            }
		   update_vehicle_state();//to update all inputs data
		   //print_vehicle_state(); //to print the all data with new set values
}

}
	return 0;
	}

void print_menu()
{
	setvbuf(stdout, NULL, _IONBF, 0);
	printf("%c .Turn On The Vehicle Engine \n ",TurnONTheVehicle);
	printf("%c .Turn Off The Vehicle Engine \n ",TurnOFFTheVehicle);
	printf("%c .Quite The System \n ",QuiteTheSystem);

}
void print_sensors_menu()
{
	setvbuf(stdout, NULL, _IONBF, 0);
	printf("%c .Turn Off The Engine \n",Turnofftheengine);
    printf("%c .Set the traffic light color.\n",Setthetrafficlightcolor);
    printf("%c .Set the room temperature (Temperature Sensor) \n ",Settheroomtemperature);
    printf("%c .Set the engine temperature (Engine Temperature Sensor) \n",Settheenginetemperature);

}
void print_vehicle_state()
{
printf("The Current Vehicle State is : \n");
printf("Engine state: %c\n", vehicle.Engine);
printf("AC: %c\n", vehicle.AC);
printf("Vehicle speed: %d km/h\n", vehicle.vehicleSpeed);
printf("Room temperature: %d °C\n", vehicle.RoomTempreture);
#if WITH_ENGINE_TEMP_CONTROLLER //check if the engine temp is enabled
    printf("Engine temperature controller state: %c\n", vehicle.EngTempController);
#endif
    printf("Engine temperature: %d °C\n\n", vehicle.EngineTemp);
}
void update_vehicle_state()
{

	if(traffic_light==green)
	{
		vehicle.vehicleSpeed=speedHIGH;
	}
	else if(traffic_light==red)
	{
		vehicle.vehicleSpeed=speedLow;
	}
	else if(traffic_light==orange)
	{
		vehicle.vehicleSpeed=speedZERO;
	}
	if(vehicle.RoomTempreture<LowRoomTEMP)
	{
		vehicle.AC='N';
		vehicle.RoomTempreture=defaultROOMTEMP;
	}
	else if(vehicle.RoomTempreture>HighRoomTEMP)
	{
		vehicle.AC='N';
		vehicle.RoomTempreture=defaultROOMTEMP;
	}
	else
	{
		vehicle.AC='F';
     }
#if  WITH_ENGINE_TEMP_CONTROLLER
	if(vehicle.EngineTemp < LowEngineTEMP)
	{
		vehicle.EngTempController='N';
		vehicle.EngineTemp=defaultENGINETEMPS;
	}
	else if(vehicle.EngineTemp > HighEngineTEMP)
	{
		vehicle.EngTempController='N';
		vehicle.EngineTemp=defaultENGINETEMPS;
	}
	else
	{
		vehicle.EngTempController='F';
	}
#endif
	if(vehicle.vehicleSpeed==speedLow)
	{
		vehicle.AC='N';
		vehicle.RoomTempreture=vehicle.RoomTempreture*(5/4)+1;
	}
#if WITH_ENGINE_TEMP_CONTROLLER
	if(vehicle.vehicleSpeed==speedLow)
	{
		vehicle.EngTempController='N';
		Vehicle.RoomTempreture=vehicle.RoomTempreture*(5/4)+1;

	}
#endif


}
void get_input()
{
	setvbuf(stdout, NULL, _IONBF, 0);

	 printf("Enter your choice: ");
		    scanf(" %c",&input);
}

