# Mete
In this project, my group and I were instructed to get creative with a platform styled game. The only restriction was that it must be a platformer, so the rest was up to us. 

Planning process
My group, Charizard, decided that we wanted something open and entertaining. Artistically it would capture the gamers attention, and technically it would be fun to play. We also thought of diversity in the game and how we might implement all our ideas. 
The game would be a dungeon crawler! This would add to the mystery behind the game. It would even include a main character that our artists created. We wanted to have a character that was ours and had its own twist to it. The character had two different styles within the game. This way we were including both artists artwork. Visually, the change was implemented using portals. For instance, once our main character entered the first portal it changed to the next artist’s character. Both artists created a level for their character. Therefore, the aesthetic of their character would match the background. In the end, we added demonic dogs and blobs as enemies for the game. This added to the overall theme of the game. To end, we wanted something simple.  In order to complete the game, you must either evade or kill the remaining demon dogs on this level. After the completion of this task, you are given a portal to the beautiful end credits. Both artists combined their skills and designed our end credits. 


Gameplay & Code 
The game starts you off with a title screen of the game’s title. Next, is a control screen which shows you how to maneuver on the game. Once you get the controls, you can start the game. You will go from one end of the platform to the other, and you must defeat at least one enemy demon dog before you reach the portal. When you reach that portal, leap through to access the pixel world. Once in the pixel world, make you way up and defeat the blob enemies. If unable to defeat them, you will still be able to access the portal at the top right of this level. After you access the portal, you will be sent to the third and final level. In this level, the demonic dogs will return. Defeat them to make it to the Bon-fire. Completion of this course will open a final screen. This final screen will display the creator information on the development of the game. 
¬Hero
Alarm_0 -  
hit = false;

Alarm_1 - 
if(image_alpha = 1.0)
	image_alpha = 0.3;
else
	image_alpha = 1.0;
	
if(hit)
	alarm[1] = 2;



Collision_2
//with(other)
//{
	//if(open)
		//room_goto_next();
//}

Collision_9
if(hit == false){
	if(hp == 1)
	{
		x = xstart;
		y = ystart;
		hp = 5;
	}
	else{
		playerRecoil=3;
		hp--;
		hit = true;
		alarm[0] = 4*room_speed;
		alarm[1] = 1;
	}
}






Create_0
hp = 5;
cooldown = 0;

//Basic Movement Starter
normalSpeed = 15
jumpSpeed = 30
normalGravity = 1
depth = -1

//Recoil Starter
recoilSpeed=10;
playerRecoil=-1;
playerStop=-1;
hit = false;


Step_0
// keep me out of things horizontally
if place_meeting(x+hspeed, y, wall) {
    if hspeed < 0 {  // i'm about to hit on the left
        move_contact_solid(180, hspeed)
    }
    else { // i'm about to hit on the right
        move_contact_solid(0, hspeed)
    }
    hspeed = 0
}


// keep me out of things vertically
if place_meeting(x, y+vspeed, wall) {
    if vspeed < 0 {  // i'm about to hit on the top
        move_contact_solid(90, vspeed)
    }
    else {  // i'm about to hit on the bottom
        move_contact_solid(270, vspeed)
        gravity = 0
    }
    vspeed = 0
}
// if i'm off the ground, give me gravity
else if !place_meeting(x, y+normalGravity, wall) {
    gravity = normalGravity
}


//Recoil
if(hit == true){

	if(playerRecoil!=-1){
	   playerRecoil-=1;
	   direction = image_angle-180; //opposite direction that the player is currently facing
	   if(hero.x < obj_enemy_OLD_ONE.x) && (!place_meeting(x-recoilSpeed, y, wall)){
			move_contact_solid(180, recoilSpeed);
	   }
		else if(hero.x > obj_enemy_OLD_ONE.x) && (!place_meeting(x+recoilSpeed, y, wall))
			move_contact_solid(0, -recoilSpeed);
	   playerStop=1;

	}

	if(playerRecoil=-1 && playerStop=1){		
		playerStop=-1;
	}
}
else{
	if(image_alpha != 1.0)
		image_alpha = 1.0;
		
	// moving right
	if keyboard_check_direct(ord("D")) {
	    // is there space for me to move right?
	    if !place_meeting(x+normalSpeed, y, wall) {
	        hspeed = normalSpeed
			image_xscale = 1;
	    }
		
	}
	// moving left
	if keyboard_check_direct(ord("A")) {
	    // is there space for me to move left?
	    if !place_meeting(x-normalSpeed, y, wall) {
	        hspeed = -normalSpeed
			image_xscale = -1;
	    }

	}

	// jumping
	// am i on the ground, and is there space above my head to jump?
	if keyboard_check_pressed(vk_space) and place_meeting(x, y+normalGravity, wall)
	and !place_meeting(x, y-jumpSpeed, wall) {
	    vspeed = -jumpSpeed
	}

	
	//Shoot Arrow
	if(mouse_check_button_pressed(mb_left) && (cooldown < 1))
	{
		instance_create_layer(x, y, "Arrow_Layer", obj_arrow); // creates bullet
		cooldown = 10; // three frame cooldown
	}
	cooldown -= 1; //reduce cooldown time
	
}

// friction to slow me down horizontally
hspeed *= .9

//Stay in Room
x = clamp(x, 0, room_width - sprite_width);

if(y > room_height)
{
	x = xstart;
	y = ystart;
}

Arrow
Collision_6d
instance_destroy();

Collision_6e
with (other) // affect instance bullet collides with
{
	hp = hp - 1; // decrease health by 1
}

instance_destroy();

Create_0
// Set Up Motion
if(hero.image_xscale == 1)
	direction = point_direction(hero.x, hero.y, x, y);
else
	direction = point_direction(hero.x, hero.y, -x, y);

speed = 16; // set speed per frame
image_xscale = hero.image_xscale; // angled in direction of travel

//Out of Bounds Set Up
cam = view_camera[0];


step_0
cam_x1 = camera_get_view_x(cam);
cam_x2 = cam_x1 + camera_get_view_width(cam);

if(x < cam_x1 || x > cam_x2)
	instance_destroy();

Arrow pixel
Collision_7
with (other) // affect instance bullet collides with
{
	hp = hp - 1; // decrease health by 1
}

instance_destroy();

Collision_c
instance_destroy();





Create_0
// Set Up Motion
if(obj_pxl.image_xscale == 1)
	direction = point_direction(obj_pxl.x, obj_pxl.y, x, y);
else
	direction = point_direction(obj_pxl.x, obj_pxl.y, -x, y);

speed = 16; // set speed per frame
image_xscale = obj_pxl.image_xscale; // angled in direction of travel

//Out of Bounds Set Up
cam = view_camera[0];

Step_0
cam_x1 = camera_get_view_x(cam);
cam_x2 = cam_x1 + camera_get_view_width(cam);

if(x < cam_x1 || x > cam_x2)
	instance_destroy();


