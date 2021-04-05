# Selection of Material Design Icons for openHASP

![kép](https://user-images.githubusercontent.com/1550668/112620845-53765780-8e29-11eb-8da8-3f1ceb934ca9.png)<br>
![kép](https://user-images.githubusercontent.com/1550668/112620966-786aca80-8e29-11eb-8e9c-228f794586bb.png)<br>
![kép](https://user-images.githubusercontent.com/1550668/112621038-920c1200-8e29-11eb-97c0-0a9d162a4dcd.png)

I've made a selection of practical icons from [Material Design Icons](https://materialdesignicons.com/). These can't be included directly whith alphanumeric fonts in the same file because their location on the codeplane starts way up above 0x10000 which cannot be addressed by hasp-lvgl. The glyphs have been moved down to the ascii address space but this would conflict with the normal characters.

Conflict is not a problem unless you don't use the same font size number for text and icons. I've prepared the icon font files for inclusion in the firmware at sizes 26, 30 and 34. These can be added in addition to the existing fonts so one can use a combination of these and the pre-included fontawesome icons too.<br>Tested on Lanbon L8 with hasp-lvgl 0.4.0.

### How to add the icons to the firmware

Example below for font size 26.

Copy `materialdesign_26.c` file to the `hasp-lvgl/src/font` directory. 

Edit the file `hasp-lvgl/include/lv_conf_v7.h`:

Search for the area where the original fonts are declared, like `#define LV_FONT_CUSTOM_28`. Add your icon font with:
```
#define LV_FONT_CUSTOM_26     LV_FONT_DECLARE(materialdesign_26)
```
Also add to `LV_FONT_CUSTOM_DECLARE` your custom font, should look something like this:
```
#define LV_FONT_CUSTOM_DECLARE LV_FONT_CUSTOM_12 \
                               LV_FONT_CUSTOM_16 \
                               LV_FONT_CUSTOM_22 \
                               LV_FONT_CUSTOM_28 \
                               LV_FONT_CUSTOM_26 \
```


Edit the file `hasp-lvgl/src/hasp/hasp_attribute.cpp`:

Search for the function `static lv_font_t* haspPayloadToFont(const char* payload)` and add your custom-sized 26 font:
```
#ifdef LV_FONT_CUSTOM_26
        case 26:
            LOG_WARNING(TAG_ATTR, "%s %d %x", __FILE__, __LINE__, materialdesign_26);
            return &materialdesign_26;
#endif
```
Wacth for proper `#endif`s at the end of the function!!!

Compile the firnware with platformio as usual, and flash it OTA to your device. To display the desired icon, simply use your custom font size (in our example 26): `p4b1.text_font=26`, and in the `jsonl` command specify the escaped character code from the table below:

| Icon | Character code | Description 
| -- | -- | --
| ![kép](https://user-images.githubusercontent.com/1550668/112601640-f96a9780-8e12-11eb-8b5e-9e139cdce82c.png) | \u0065 | arrow down
| ![kép](https://user-images.githubusercontent.com/1550668/112602206-ab09c880-8e13-11eb-9a01-ac8ae774375e.png) | \u007d | arrow up
| ![kép](https://user-images.githubusercontent.com/1550668/112602286-c1b01f80-8e13-11eb-86c1-151297c42082.png) | \u006d | arrow left
| ![kép](https://user-images.githubusercontent.com/1550668/112602326-cecd0e80-8e13-11eb-84a4-89794d128165.png) | \u0074 | arrow right
| ![kép](https://user-images.githubusercontent.com/1550668/112603048-bc9fa000-8e14-11eb-92fc-5f9894abffa1.png) | \u06e3 | arrow-up-box
| ![kép](https://user-images.githubusercontent.com/1550668/112609991-7f3f1080-8e1c-11eb-90f6-fa824f5b4a4b.png) | \u06e0 | arrow-down-box
| ![kép](https://user-images.githubusercontent.com/1550668/112603107-d04b0680-8e14-11eb-964a-a3392fddf94c.png) | \u06e1 | arrow-left-box
| ![kép](https://user-images.githubusercontent.com/1550668/112603142-de992280-8e14-11eb-9bac-62dd62137aa1.png) | \u06e2 | arrow-right-box
| ![kép](https://user-images.githubusercontent.com/1550668/112602394-e5736580-8e13-11eb-98af-59081b367f7a.png) | \u0160 | chevron down
| ![kép](https://user-images.githubusercontent.com/1550668/112602450-fd4ae980-8e13-11eb-9651-606014d168a3.png) | \u0161 | chevron left
| ![kép](https://user-images.githubusercontent.com/1550668/112602478-0936ab80-8e14-11eb-9abe-a18becdc1731.png) | \u0162 | chevron right
| ![kép](https://user-images.githubusercontent.com/1550668/112602516-1358aa00-8e14-11eb-83d3-179428948db5.png) | \u0163 | chevron up
| ![kép](https://user-images.githubusercontent.com/1550668/112603414-42bbe680-8e15-11eb-9217-3b846d89d9df.png) | \u037d | menu-down
| ![kép](https://user-images.githubusercontent.com/1550668/112603445-4e0f1200-8e15-11eb-8b1d-b971da582020.png) | \u037e | menu-left
| ![kép](https://user-images.githubusercontent.com/1550668/112603469-58311080-8e15-11eb-8e1e-b2e11bb6040a.png) | \u037f | menu-right
| ![kép](https://user-images.githubusercontent.com/1550668/112603495-63843c00-8e15-11eb-8434-3a0925359dbf.png) | \u0380 | menu-up
| ![kép](https://user-images.githubusercontent.com/1550668/112604191-2a989700-8e16-11eb-81fd-6b485910d68e.png) | \u0435 | plus
| ![kép](https://user-images.githubusercontent.com/1550668/112604245-33896880-8e16-11eb-843f-f4d20f5d7686.png) | \u0394 | minus
| ![kép](https://user-images.githubusercontent.com/1550668/112607306-5b2e0000-8e19-11eb-83d3-cac0094e24b1.png) | \u0437 | plus-circle
| ![kép](https://user-images.githubusercontent.com/1550668/112607391-7436b100-8e19-11eb-87b1-fbf7d9aabcc2.png) | \u0396 | minus-circle
| ![kép](https://user-images.githubusercontent.com/1550668/112607352-6719c200-8e19-11eb-90b9-297fc9166dd6.png) | \u0436 | plus-box
| ![kép](https://user-images.githubusercontent.com/1550668/112607434-7f89dc80-8e19-11eb-8eeb-4f1d18daac4f.png) | \u0395 | minus-box
| ![kép](https://user-images.githubusercontent.com/1550668/112606281-79473080-8e18-11eb-9434-628d816637ba.png) | \u014c | check
| ![kép](https://user-images.githubusercontent.com/1550668/112606311-82d09880-8e18-11eb-99b9-911ff7173432.png) | \u0601 | check-circle-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112606342-8d8b2d80-8e18-11eb-898a-c512d721ccf6.png) | \u0c72 | check-box-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112606364-95e36880-8e18-11eb-9172-a019ec848055.png) | \u04b3 | cog
| ![kép](https://user-images.githubusercontent.com/1550668/112606395-a09dfd80-8e18-11eb-9648-ed565d61ede6.png) | \u066e | info
| ![kép](https://user-images.githubusercontent.com/1550668/112602593-2e2b1e80-8e14-11eb-9a46-b6beaf1ac37d.png) | \u0355 | lightbulb
| ![kép](https://user-images.githubusercontent.com/1550668/112602634-3aaf7700-8e14-11eb-802e-81abd2af1a8a.png) | \u0356 | lightbulb-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112608099-35552b00-8e1a-11eb-92a6-315ea28c5b01.png) | \u0708 | lightbulb-on
| ![kép](https://user-images.githubusercontent.com/1550668/112608123-3d14cf80-8e1a-11eb-8184-07d377d7941f.png) | \u0709 | lightbulb-on-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112604790-db069b00-8e16-11eb-9416-03a844f45554.png) | \u06c5 | power-plug
| ![kép](https://user-images.githubusercontent.com/1550668/112604833-e5c13000-8e16-11eb-93ef-526ab3d76df3.png) | \u06c6 | power-plug-off
| ![kép](https://user-images.githubusercontent.com/1550668/112604861-ef4a9800-8e16-11eb-891d-0ac1be573a7c.png) | \u0445 | power
| ![kép](https://user-images.githubusercontent.com/1550668/112602682-49962980-8e14-11eb-8f78-ddabc6e616cb.png) | \u0458 | heater-on
| ![kép](https://user-images.githubusercontent.com/1550668/112602722-53b82800-8e14-11eb-844b-dc1217efc0cd.png) | \u0af7 | heater
| ![kép](https://user-images.githubusercontent.com/1550668/112602750-5dda2680-8e14-11eb-86dd-4c9672c9a345.png) | \u0af8 | heater-off
| ![kép](https://user-images.githubusercontent.com/1550668/112604287-3dab6700-8e16-11eb-9d13-e0b9a6012ebf.png) | \u083b | door-closed
| ![kép](https://user-images.githubusercontent.com/1550668/112604313-469c3880-8e16-11eb-9715-0afabb5b551c.png) | \u10cf | door-closed-lock
| ![kép](https://user-images.githubusercontent.com/1550668/112604349-5156cd80-8e16-11eb-9dab-05430fadb59e.png) | \u083c | door-open
| ![kép](https://user-images.githubusercontent.com/1550668/112604526-895e1080-8e16-11eb-8c09-2c7b4290c955.png) | \u0541 | toggle-switch
| ![kép](https://user-images.githubusercontent.com/1550668/112604555-93800f00-8e16-11eb-8087-2abf445d6775.png) | \u0542 | toggle-switch-off
| ![kép](https://user-images.githubusercontent.com/1550668/112604595-9ed33a80-8e16-11eb-8c88-f1ed11972e83.png) | \u00ba | bell
| ![kép](https://user-images.githubusercontent.com/1550668/112603223-fec8e180-8e14-11eb-93dd-769c84d478b0.png) | \u113c | window shutter closed
| ![kép](https://user-images.githubusercontent.com/1550668/112603260-0ab4a380-8e15-11eb-85c5-b1559d985f5d.png) | \u113d | window shutter warning
| ![kép](https://user-images.githubusercontent.com/1550668/112603287-156f3880-8e15-11eb-9248-239b45f2c91d.png) | \u113e | window shutter open
| ![kép](https://user-images.githubusercontent.com/1550668/112603171-ea84e480-8e14-11eb-9224-47e584a87d1c.png) | \u06f9 | garage closed
| ![kép](https://user-images.githubusercontent.com/1550668/112603197-f40e4c80-8e14-11eb-8304-4e3b5595433f.png) | \u06fa | garage open
| ![kép](https://user-images.githubusercontent.com/1550668/112610031-89f9a580-8e1c-11eb-92ea-ce7caa099650.png) | \u12f3 | garage-variant
| ![kép](https://user-images.githubusercontent.com/1550668/112610076-94b43a80-8e1c-11eb-9832-c48d50d16372.png) | \u12f4 | garage-open-variant
| ![kép](https://user-images.githubusercontent.com/1550668/112604467-75b2aa00-8e16-11eb-89c4-51cfb5417264.png) | \u035e | lock
| ![kép](https://user-images.githubusercontent.com/1550668/112604496-7fd4a880-8e16-11eb-8d7a-f46cf7e5fd1a.png) | \u0fe6 | lock-open-variant
| ![kép](https://user-images.githubusercontent.com/1550668/112605399-8dd6f900-8e17-11eb-9460-bbff85df74c7.png) | \u032b | key-variant
| ![kép](https://user-images.githubusercontent.com/1550668/112604381-5d428f80-8e16-11eb-8004-b62016ecb41c.png) | \u0228 | eye
| ![kép](https://user-images.githubusercontent.com/1550668/112604430-6a5f7e80-8e16-11eb-8d80-22a6c8711726.png) | \u0229 | eye-off
| ![kép](https://user-images.githubusercontent.com/1550668/112607816-e60efa80-8e19-11eb-9d04-f5a34578eb87.png) | \u0e66 | hand-left
| ![kép](https://user-images.githubusercontent.com/1550668/112609893-633b6f00-8e1c-11eb-8f3e-91cf0eaea5bf.png) | \u0046 | alert
| ![kép](https://user-images.githubusercontent.com/1550668/112605323-7861cf00-8e17-11eb-9560-42dbe8608504.png) | \u02fc | home
| ![kép](https://user-images.githubusercontent.com/1550668/112605354-8283cd80-8e17-11eb-97d7-1de87e58d188.png) | \u07f0 | home-assistant
| ![kép](https://user-images.githubusercontent.com/1550668/112603389-38015180-8e15-11eb-8907-933f5a39e6b5.png) | \u06c1 | home-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112610117-9ed63900-8e1c-11eb-9a2f-658943c320d1.png) | \u02fe | home-variant
| ![kép](https://user-images.githubusercontent.com/1550668/112610146-a7c70a80-8e1c-11eb-91b2-6ccbadd372ce.png) | \u0bc7 | home-variant-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112610180-b1e90900-8e1c-11eb-867c-3a4c9b56f133.png) | \u0ceb | shield-home-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112603529-6bdc7700-8e15-11eb-86fe-e11e703f8f0d.png) | \u042e | play-pause
| ![kép](https://user-images.githubusercontent.com/1550668/112603555-75fe7580-8e15-11eb-91ac-51eb3b3a2c74.png) | \u042a | play
| ![kép](https://user-images.githubusercontent.com/1550668/112603579-7eef4700-8e15-11eb-9774-7a5c033c4213.png) | \u0404 | pause
| ![kép](https://user-images.githubusercontent.com/1550668/112603634-8f072680-8e15-11eb-97b8-f03746b0c5ca.png) | \u04fb | stop
| ![kép](https://user-images.githubusercontent.com/1550668/112603660-98908e80-8e15-11eb-9ada-365515c9fa29.png) | \u0231 | fast-forward
| ![kép](https://user-images.githubusercontent.com/1550668/112603689-a3e3ba00-8e15-11eb-80f9-925e709193d0.png) | \u047f | rewind
| ![kép](https://user-images.githubusercontent.com/1550668/112603724-ae05b880-8e15-11eb-93a8-473dc5e1fc4c.png) | \u04cd | skip-next
| ![kép](https://user-images.githubusercontent.com/1550668/112603763-b6f68a00-8e15-11eb-98f6-ce3f58450405.png) | \u04ce | skip-previous
| ![kép](https://user-images.githubusercontent.com/1550668/113571517-d0b67f00-9616-11eb-816f-810a6b55b6d5.png) | \u0476 | repeat
| ![kép](https://user-images.githubusercontent.com/1550668/113571532-d744f680-9616-11eb-8ed5-26dbc23050fb.png) | \u0477 | repeat-off
| ![kép](https://user-images.githubusercontent.com/1550668/113571554-df049b00-9616-11eb-9697-c4742e0ffcad.png) | \u0478 | repeat-once
| ![kép](https://user-images.githubusercontent.com/1550668/113571567-e9bf3000-9616-11eb-816d-e05be9aa0f5b.png) | \u04BD | shuffle
| ![kép](https://user-images.githubusercontent.com/1550668/113571584-f2176b00-9616-11eb-82f4-7f799e3cbaa6.png) | \u04BE | shuffle-disabled
| ![kép](https://user-images.githubusercontent.com/1550668/112603885-df7e8400-8e15-11eb-891f-73e9e6de7a35.png) | \u077a | music
| ![kép](https://user-images.githubusercontent.com/1550668/112603943-ef966380-8e15-11eb-99f7-e05503f8af8c.png) | \u059e | volume-high
| ![kép](https://user-images.githubusercontent.com/1550668/112603974-f7ee9e80-8e15-11eb-8430-03dbd224356f.png) | \u059f | volume-low
| ![kép](https://user-images.githubusercontent.com/1550668/112604010-02109d00-8e16-11eb-85e1-cdd691c9e1fb.png) | \u05a0 | volume-medium
| ![kép](https://user-images.githubusercontent.com/1550668/112604058-0b9a0500-8e16-11eb-992b-3785e033f3f7.png) | \u077f | volume-mute
| ![kép](https://user-images.githubusercontent.com/1550668/112604093-15bc0380-8e16-11eb-86dc-443a092516d2.png) | \u038c | microphone
| ![kép](https://user-images.githubusercontent.com/1550668/112604143-20769880-8e16-11eb-98a6-67dd706e5901.png) | \u038d | microphone-off
| ![kép](https://user-images.githubusercontent.com/1550668/112604966-0f7a5700-8e17-11eb-803a-6ce3cf71bd81.png) | \u0522 | television
| ![kép](https://user-images.githubusercontent.com/1550668/112607635-b6f88900-8e19-11eb-9c7c-340efe542a08.png) | \u0459 | radio
| ![kép](https://user-images.githubusercontent.com/1550668/112607677-bfe95a80-8e19-11eb-810c-fb0eec8bbb1b.png) | \u04e3 | speaker
| ![kép](https://user-images.githubusercontent.com/1550668/112607733-c972c280-8e19-11eb-9e6b-c2d5c8ae1cee.png) | \u04e4 | speaker-off
| ![kép](https://user-images.githubusercontent.com/1550668/112607775-d2fc2a80-8e19-11eb-9fbd-4a4e0d637d04.png) | \u0f7f | monitor-speaker
| ![kép](https://user-images.githubusercontent.com/1550668/112604928-05585880-8e17-11eb-81c5-62a221626c04.png) | \u064e | tune (settings)
| ![kép](https://user-images.githubusercontent.com/1550668/112604635-aabefc80-8e16-11eb-8235-2f9b1fdeca1c.png) | \u0399 | monitor
| ![kép](https://user-images.githubusercontent.com/1550668/112604739-c7f3cb00-8e16-11eb-9004-f035e0e70c0f.png) | \u0342 | laptop
| ![kép](https://user-images.githubusercontent.com/1550668/112604767-d17d3300-8e16-11eb-81cc-efacd94dda1d.png) | \u013c | cellphone
| ![kép](https://user-images.githubusercontent.com/1550668/112602997-a85ba300-8e14-11eb-9f0a-7d7acd5e9ab6.png) | \u07e0 | desktop-classic
| ![kép](https://user-images.githubusercontent.com/1550668/112604991-199c5580-8e17-11eb-9fa6-2ef85762c361.png) | \u05c9 | wifi
| ![kép](https://user-images.githubusercontent.com/1550668/112609934-6c2c4080-8e1c-11eb-9e82-142c1ae58f0d.png) | \u1139 | antenna
| ![kép](https://user-images.githubusercontent.com/1550668/112604895-fa9dc380-8e16-11eb-99de-afa9743f9913.png) | \u04c2 | signal
| ![kép](https://user-images.githubusercontent.com/1550668/113571476-bda3af00-9616-11eb-9f52-0d46c8b2e376.png) | \u00CF | bluetooth
| ![kép](https://user-images.githubusercontent.com/1550668/113571502-c72d1700-9616-11eb-9779-7536d38f8ece.png) | \u00D0 | bluetooth-audio
| ![kép](https://user-images.githubusercontent.com/1550668/112605026-2325bd80-8e17-11eb-8d24-e2311f203923.png) | \u09c0 | shower-bath
| ![kép](https://user-images.githubusercontent.com/1550668/112605058-2c168f00-8e17-11eb-91ca-efe8c472c220.png) | \u0303 | bed
| ![kép](https://user-images.githubusercontent.com/1550668/112605096-3769ba80-8e17-11eb-893c-4f8767629e0c.png) | \u12f1 | sleep
| ![kép](https://user-images.githubusercontent.com/1550668/112605143-4486a980-8e17-11eb-819d-2db58b1925b4.png) | \u04d9 | sofa
| ![kép](https://user-images.githubusercontent.com/1550668/112605179-4fd9d500-8e17-11eb-9fd2-4e4146775354.png) | \u0612 | food-fork-drink
| ![kép](https://user-images.githubusercontent.com/1550668/112605286-6f70fd80-8e17-11eb-91f2-51b679e03a20.png) | \u0196 | coffee
| ![kép](https://user-images.githubusercontent.com/1550668/112607795-dc859280-8e19-11eb-8485-bc66ad98e663.png) | \u0b9c | chef-hat
| ![kép](https://user-images.githubusercontent.com/1550668/112605529-b101a880-8e17-11eb-9291-8335883361a6.png) | \u0a99 | trash-can
| ![kép](https://user-images.githubusercontent.com/1550668/112605222-5b2d0080-8e17-11eb-86d8-3603f6be3c22.png) | \u09cb | toilet
| ![kép](https://user-images.githubusercontent.com/1550668/112605447-9a5b5180-8e17-11eb-8367-0cecf85ad442.png) | \u0217 | poo
| ![kép](https://user-images.githubusercontent.com/1550668/112605253-654eff00-8e17-11eb-945b-92f4ab41efd0.png) | \u012b | car
| ![kép](https://user-images.githubusercontent.com/1550668/112605492-a6dfaa00-8e17-11eb-8733-a0c114a33439.png) | \u0626 | pool
| ![kép](https://user-images.githubusercontent.com/1550668/112605578-bfe85b00-8e17-11eb-9ce3-7d591c94c9d5.png) | \u052f | thermometer
| ![kép](https://user-images.githubusercontent.com/1550668/112605618-cb3b8680-8e17-11eb-901a-cf5ed06b0c42.png) | \u10e2 | thermometer-high
| ![kép](https://user-images.githubusercontent.com/1550668/112605654-d4c4ee80-8e17-11eb-9821-0348eb47e12d.png) | \u10e3 | thermometer-low
| ![kép](https://user-images.githubusercontent.com/1550668/112605697-de4e5680-8e17-11eb-815d-9cb7779ce30b.png) | \u1551 | thermometer-off
| ![kép](https://user-images.githubusercontent.com/1550668/112605760-eefecc80-8e17-11eb-91f7-81f6580c00af.png) | \u05ae | water-percent
| ![kép](https://user-images.githubusercontent.com/1550668/112605827-02aa3300-8e18-11eb-9c62-90f78569883c.png) | \u05b0 | weather-cloudy
| ![kép](https://user-images.githubusercontent.com/1550668/112605863-0c339b00-8e18-11eb-9de2-26da56d5d9e1.png) | \u05b2 | weather-hail
| ![kép](https://user-images.githubusercontent.com/1550668/112605916-1786c680-8e18-11eb-8fc3-aff86431ce31.png) | \u05b6 | weather-pouring
| ![kép](https://user-images.githubusercontent.com/1550668/112605957-22415b80-8e18-11eb-91c9-bf5ab9ce509b.png) | \u05b9 | weather-sunny
| ![kép](https://user-images.githubusercontent.com/1550668/112605997-2cfbf080-8e18-11eb-95d9-b317c55f647a.png) | \u05b5 | weather-partly-cloudy
| ![kép](https://user-images.githubusercontent.com/1550668/112606026-35ecc200-8e18-11eb-8bfa-4e3a6c002b92.png) | \u05b4 | weather-night
| ![kép](https://user-images.githubusercontent.com/1550668/112606066-400ec080-8e18-11eb-9f4a-371ae05d33d5.png) | \u0f51 | weather-night-partly-cloudy
| ![kép](https://user-images.githubusercontent.com/1550668/112606106-4a30bf00-8e18-11eb-9cbb-b53d46ee02ab.png) | \u05b1 | weather-fog
| ![kép](https://user-images.githubusercontent.com/1550668/112606136-53219080-8e18-11eb-8548-db20cbb356f7.png) | \u05bd | weather-windy
| ![kép](https://user-images.githubusercontent.com/1550668/112606173-5d438f00-8e18-11eb-86fd-e912601ebbb6.png) | \u0737 | snowflake
| ![kép](https://user-images.githubusercontent.com/1550668/112606209-66ccf700-8e18-11eb-9ad4-3169bbcba5fe.png) | \u056a | umbrella
| ![kép](https://user-images.githubusercontent.com/1550668/112607543-9af4e780-8e19-11eb-9825-c457f99d834b.png) | \u034a | leaf
| ![kép](https://user-images.githubusercontent.com/1550668/112607569-a5af7c80-8e19-11eb-9062-d0a9e45367de.png) | \u0425 | pine-tree
| ![kép](https://user-images.githubusercontent.com/1550668/112608053-2b332c80-8e1a-11eb-946b-73fa5ae9a1d5.png) | \u0611 | ev-station
| ![kép](https://user-images.githubusercontent.com/1550668/112609960-751d1200-8e1c-11eb-91c6-e91a4cbbff7d.png) | \u142b | lightning-bolt
| ![kép](https://user-images.githubusercontent.com/1550668/112605787-f7ef9e00-8e17-11eb-8633-b7511f56b599.png) | \u0261 | flash
| ![kép](https://user-images.githubusercontent.com/1550668/112607838-ee673580-8e19-11eb-8fb1-8994d9d7b562.png) | \u02f1 | heart
| ![kép](https://user-images.githubusercontent.com/1550668/112607157-3043ac00-8e19-11eb-8384-03cc74def418.png) | \u04ee | star
| ![kép](https://user-images.githubusercontent.com/1550668/112607225-43ef1280-8e19-11eb-9ade-3771c76b21f5.png) | \u0851 | shape
| ![kép](https://user-images.githubusercontent.com/1550668/113571610-fc396980-9616-11eb-973e-f0c995878b5c.png) | \u0EB5 | circle-double
| ![kép](https://user-images.githubusercontent.com/1550668/112606251-6fbdc880-8e18-11eb-9baf-dbf838b0ccd1.png) | \u008e | backspace
| ![kép](https://user-images.githubusercontent.com/1550668/112606479-b0b5dd00-8e18-11eb-9b78-e2337df013fc.png) | \u066a | human-greeting
| ![kép](https://user-images.githubusercontent.com/1550668/112606655-ba3f4500-8e18-11eb-9b1a-efcfe21c49a5.png) | \u0024 | account
| ![kép](https://user-images.githubusercontent.com/1550668/112606817-c4614380-8e18-11eb-90c0-771bbc16a411.png) | \u0be8 | skull-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112607191-3c2f6e00-8e19-11eb-99f7-faf4158e1c5a.png) | \u05a9 | watch
| ![kép](https://user-images.githubusercontent.com/1550668/112607604-ae07b780-8e19-11eb-8a01-2b639f3a7284.png) | \u0170 | clock-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112607270-4f423e00-8e19-11eb-8ba8-44ed2cf20b7e.png) | \u1759 | chat-question-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112607869-f8893400-8e19-11eb-8e25-e3cd03a99802.png) | \u00ae | battery-outline
| ![kép](https://user-images.githubusercontent.com/1550668/112607898-0343c900-8e1a-11eb-9623-c6df0283d7ba.png) | \u12c1 | battery-low
| ![kép](https://user-images.githubusercontent.com/1550668/112607945-0c349a80-8e1a-11eb-82b4-bd205d172eba.png) | \u12c2 | battery-medium
| ![kép](https://user-images.githubusercontent.com/1550668/112607986-16ef2f80-8e1a-11eb-98ff-570307067fe3.png) | \u12c3 | battery-high
| ![kép](https://user-images.githubusercontent.com/1550668/112608017-21112e00-8e1a-11eb-9fa3-f2ce3f49550b.png) | \u0369 | magnify

