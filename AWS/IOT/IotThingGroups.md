#### [Back](./README.md)

# AWS IOT Thing Groups (Static VS Dynamic)

AWS IOT Thing Group is a logical group of things to manage several things.

There are two type of Thing Group supported by AWS IOT Core

**Static Thing Group:-**
A static Thing Group can contain the several things as well as other static group, the devices are added once can not be updated during any on going operation 
Like OTA,

**Dynamic Thing Group:-**
On the other hand Dynamic Thing group is a group where we can add multiple things by define a query condition.
Ex:-  During the OTA Update the list of devices are fixed if we create the OTA on Static Thing Group while if we pass a query to create a dynamic group like do OTA only on devices which is online.

Command to create a Static Group:-

    aws iot create-thing-group --thing-group-name TestStaticGroup


Command to create a Dynamic Group:-
    
    aws iot create-dynamic-thing-group --thing-group-name "RoomTooWarm" --query-string "attributes.temperature>60"


Command to add thing in Static Group:-
    
    aws iot add-thing-to-thing-group --thing-name MyLightBulb --thing-group-name RedLights


Command to Delete a Static Group:-
    
    aws iot delete-thing-group --thing-group-name "RedLights"


Command to Delete a Dynamic Group:-
    
    aws iot delete-dynamic-thing-group --thing-group-name "RoomTooWarm"