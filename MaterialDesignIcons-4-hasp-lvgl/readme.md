# Selection of Material Design Icons for openHASP

![kép](https://user-images.githubusercontent.com/1550668/112620845-53765780-8e29-11eb-8da8-3f1ceb934ca9.png)<br>
![kép](https://user-images.githubusercontent.com/1550668/112620966-786aca80-8e29-11eb-8e9c-228f794586bb.png)<br>
![kép](https://user-images.githubusercontent.com/1550668/112621038-920c1200-8e29-11eb-97c0-0a9d162a4dcd.png)

I've made a selection of practical icons from [Material Design Icons](https://materialdesignicons.com/). These can't be included directly whith alphanumeric fonts in the same file because their location on the codeplane starts way up above 0x10000 which cannot be addressed by hasp-lvgl. The glyphs have been moved down by E2000 to the private use space (starting with E001).

I've prepared the icon font files for inclusion in the firmware at sizes 26, 30 and 34. These can be added in addition to the existing fonts 

Tested on Lanbon L8 with openHASP 0.4.1.

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

Compile the firnware with platformio as usual, and flash it OTA to your device. To display the desired icon, simply use your custom font size (in our example 26): `p4b1.text_font=26`, and in the `jsonl` command specify the escaped, _shifted down_ character code from the table below:

Icon  | Suggested<br>for default  | Character code<br>shifted down by E2000 | Description | Original MDI<br>codepoint
--  | --  | --  | -- | --
![kép](https://user-images.githubusercontent.com/1550668/112601640-f96a9780-8e12-11eb-8b5e-9e139cdce82c.png) | x | \uE045 | arrow down | 0xf0045
![kép](https://user-images.githubusercontent.com/1550668/112602206-ab09c880-8e13-11eb-9a01-ac8ae774375e.png) | x | \uE05D | arrow up | 0xf005d
![kép](https://user-images.githubusercontent.com/1550668/112602286-c1b01f80-8e13-11eb-86c1-151297c42082.png) | x | \uE04D | arrow left | 0xf004d
![kép](https://user-images.githubusercontent.com/1550668/112602326-cecd0e80-8e13-11eb-84a4-89794d128165.png) | x | \uE054 | arrow right | 0xf0054
![kép](https://user-images.githubusercontent.com/1550668/112603048-bc9fa000-8e14-11eb-92fc-5f9894abffa1.png) | x | \uE6C3 | arrow-up-box | 0xf06c3
![kép](https://user-images.githubusercontent.com/1550668/112609991-7f3f1080-8e1c-11eb-90f6-fa824f5b4a4b.png) | x | \uE6C0 | arrow-down-box | 0xf06c0
![kép](https://user-images.githubusercontent.com/1550668/112603107-d04b0680-8e14-11eb-964a-a3392fddf94c.png) | x | \uE6C1 | arrow-left-box | 0xf06c1
![kép](https://user-images.githubusercontent.com/1550668/112603142-de992280-8e14-11eb-9bac-62dd62137aa1.png) | x | \uE6C2 | arrow-right-box | 0xf06c2
![kép](https://user-images.githubusercontent.com/1550668/112602394-e5736580-8e13-11eb-98af-59081b367f7a.png) |  | \uE140 | chevron down | 0xf0140
![kép](https://user-images.githubusercontent.com/1550668/112602450-fd4ae980-8e13-11eb-9651-606014d168a3.png) |  | \uE141 | chevron left | 0xf0141
![kép](https://user-images.githubusercontent.com/1550668/112602478-0936ab80-8e14-11eb-9abe-a18becdc1731.png) |  | \uE142 | chevron right | 0xf0142
![kép](https://user-images.githubusercontent.com/1550668/112602516-1358aa00-8e14-11eb-83d3-179428948db5.png) |  | \uE143 | chevron up | 0xf0143
![kép](https://user-images.githubusercontent.com/1550668/112603414-42bbe680-8e15-11eb-9217-3b846d89d9df.png) | x | \uE35D | menu-down | 0xf035d
![kép](https://user-images.githubusercontent.com/1550668/112603445-4e0f1200-8e15-11eb-8b1d-b971da582020.png) | x | \uE35E | menu-left | 0xf035e
![kép](https://user-images.githubusercontent.com/1550668/112603469-58311080-8e15-11eb-8e1e-b2e11bb6040a.png) | x | \uE35F | menu-right | 0xf035f
![kép](https://user-images.githubusercontent.com/1550668/112603495-63843c00-8e15-11eb-8434-3a0925359dbf.png) | x | \uE360 | menu-up | 0xf0360
![kép](https://user-images.githubusercontent.com/1550668/112604191-2a989700-8e16-11eb-81fd-6b485910d68e.png) | x | \uE415 | plus | 0xf0415
![kép](https://user-images.githubusercontent.com/1550668/112604245-33896880-8e16-11eb-843f-f4d20f5d7686.png) | x | \uE374 | minus | 0xf0374
![kép](https://user-images.githubusercontent.com/1550668/112607306-5b2e0000-8e19-11eb-83d3-cac0094e24b1.png) |  | \uE417 | plus-circle | 0xf0417
![kép](https://user-images.githubusercontent.com/1550668/112607391-7436b100-8e19-11eb-87b1-fbf7d9aabcc2.png) |  | \uE376 | minus-circle | 0xf0376
![kép](https://user-images.githubusercontent.com/1550668/112607352-6719c200-8e19-11eb-90b9-297fc9166dd6.png) |  | \uE416 | plus-box | 0xf0416
![kép](https://user-images.githubusercontent.com/1550668/112607434-7f89dc80-8e19-11eb-8eeb-4f1d18daac4f.png) |  | \uE375 | minus-box | 0xf0375
![kép](https://user-images.githubusercontent.com/1550668/112606281-79473080-8e18-11eb-9434-628d816637ba.png) |  | \uE12C | check | 0xf012c
![kép](https://user-images.githubusercontent.com/1550668/112606311-82d09880-8e18-11eb-99b9-911ff7173432.png) |  | \uE5E1 | check-circle-outline | 0xf05e1
![kép](https://user-images.githubusercontent.com/1550668/112606342-8d8b2d80-8e18-11eb-898a-c512d721ccf6.png) |  | \uEC52 | check-box-outline | 0xf0c52
![kép](https://user-images.githubusercontent.com/1550668/112606364-95e36880-8e18-11eb-9172-a019ec848055.png) |  | \uE493 | cog | 0xf0493
![kép](https://user-images.githubusercontent.com/1550668/112606395-a09dfd80-8e18-11eb-9648-ed565d61ede6.png) |  | \uE64E | info | 0xf064e
![kép](https://user-images.githubusercontent.com/1550668/112602593-2e2b1e80-8e14-11eb-9a46-b6beaf1ac37d.png) | x | \uE335 | lightbulb | 0xf0335
![kép](https://user-images.githubusercontent.com/1550668/112602634-3aaf7700-8e14-11eb-802e-81abd2af1a8a.png) | x | \uE336 | lightbulb-outline | 0xf0336
![kép](https://user-images.githubusercontent.com/1550668/112608099-35552b00-8e1a-11eb-92a6-315ea28c5b01.png) | x | \uE6E8 | lightbulb-on | 0xf06e8
![kép](https://user-images.githubusercontent.com/1550668/112608123-3d14cf80-8e1a-11eb-8184-07d377d7941f.png) | x | \uE6E9 | lightbulb-on-outline | 0xf06e9
![kép](https://user-images.githubusercontent.com/1550668/112604790-db069b00-8e16-11eb-9416-03a844f45554.png) | x | \uE6A5 | power-plug | 0xf06a5
![kép](https://user-images.githubusercontent.com/1550668/112604833-e5c13000-8e16-11eb-93ef-526ab3d76df3.png) | x | \uE6A6 | power-plug-off | 0xf06a6
![kép](https://user-images.githubusercontent.com/1550668/112604861-ef4a9800-8e16-11eb-891d-0ac1be573a7c.png) | x | \uE425 | power | 0xf0425
![kép](https://user-images.githubusercontent.com/1550668/112602682-49962980-8e14-11eb-8f78-ddabc6e616cb.png) | x | \uE438 | heater-on | 0xf0438
![kép](https://user-images.githubusercontent.com/1550668/112602722-53b82800-8e14-11eb-844b-dc1217efc0cd.png) | x | \uEAD7 | heater | 0xf0ad7
![kép](https://user-images.githubusercontent.com/1550668/112602750-5dda2680-8e14-11eb-86dd-4c9672c9a345.png) | x | \uEAD8 | heater-off | 0xf0ad8
![kép](https://user-images.githubusercontent.com/1550668/112604287-3dab6700-8e16-11eb-9d13-e0b9a6012ebf.png) | x | \uE81B | door-closed | 0xf081b
![kép](https://user-images.githubusercontent.com/1550668/112604313-469c3880-8e16-11eb-9715-0afabb5b551c.png) | x | \uF0AF | door-closed-lock | 0xf10af
![kép](https://user-images.githubusercontent.com/1550668/112604349-5156cd80-8e16-11eb-9dab-05430fadb59e.png) | x | \uE81C | door-open | 0xf081c
![kép](https://user-images.githubusercontent.com/1550668/112604526-895e1080-8e16-11eb-8c09-2c7b4290c955.png) |  | \uE521 | toggle-switch | 0xf0521
![kép](https://user-images.githubusercontent.com/1550668/112604555-93800f00-8e16-11eb-8087-2abf445d6775.png) |  | \uE522 | toggle-switch-off | 0xf0522
![kép](https://user-images.githubusercontent.com/1550668/112604595-9ed33a80-8e16-11eb-8c88-f1ed11972e83.png) | x | \uE09A | bell | 0xf009a
![kép](https://user-images.githubusercontent.com/1550668/112603223-fec8e180-8e14-11eb-93dd-769c84d478b0.png) | x | \uF11C | window shutter closed | 0xf111c
![kép](https://user-images.githubusercontent.com/1550668/112603260-0ab4a380-8e15-11eb-85c5-b1559d985f5d.png) | x | \uF11D | window shutter warning | 0xf111d
![kép](https://user-images.githubusercontent.com/1550668/112603287-156f3880-8e15-11eb-9248-239b45f2c91d.png) | x | \uF11E | window shutter open | 0xf111e
![kép](https://user-images.githubusercontent.com/1550668/112603171-ea84e480-8e14-11eb-9224-47e584a87d1c.png) |  | \uE6D9 | garage closed | 0xf06d9
![kép](https://user-images.githubusercontent.com/1550668/112603197-f40e4c80-8e14-11eb-8304-4e3b5595433f.png) |  | \uE6DA | garage open | 0xf06da
![kép](https://user-images.githubusercontent.com/1550668/112610031-89f9a580-8e1c-11eb-92ea-ce7caa099650.png) | x | \uF2D3 | garage-variant | 0xf12d3
![kép](https://user-images.githubusercontent.com/1550668/112610076-94b43a80-8e1c-11eb-9832-c48d50d16372.png) | x | \uF2D4 | garage-open-variant | 0xf12d4
![kép](https://user-images.githubusercontent.com/1550668/112604467-75b2aa00-8e16-11eb-89c4-51cfb5417264.png) |  | \uE33E | lock | 0xf033e
![kép](https://user-images.githubusercontent.com/1550668/112604496-7fd4a880-8e16-11eb-8d7a-f46cf7e5fd1a.png) |  | \uEFC6 | lock-open-variant | 0xf0fc6
![kép](https://user-images.githubusercontent.com/1550668/112605399-8dd6f900-8e17-11eb-9460-bbff85df74c7.png) |  | \uE30B | key-variant | 0xf030b
![kép](https://user-images.githubusercontent.com/1550668/112604381-5d428f80-8e16-11eb-8004-b62016ecb41c.png) |  | \uE208 | eye | 0xf0208
![kép](https://user-images.githubusercontent.com/1550668/112604430-6a5f7e80-8e16-11eb-8d80-22a6c8711726.png) |  | \uE209 | eye-off | 0xf0209
![kép](https://user-images.githubusercontent.com/1550668/112607816-e60efa80-8e19-11eb-9d04-f5a34578eb87.png) | x | \uEE46 | hand-left | 0xf0e46
![kép](https://user-images.githubusercontent.com/1550668/112609893-633b6f00-8e1c-11eb-8f3e-91cf0eaea5bf.png) | x | \uE026 | alert | 0xf0026
![kép](https://user-images.githubusercontent.com/1550668/112605323-7861cf00-8e17-11eb-9560-42dbe8608504.png) | x | \uE2DC | home | 0xf02dc
![kép](https://user-images.githubusercontent.com/1550668/112605354-8283cd80-8e17-11eb-97d7-1de87e58d188.png) | x | \uE7D0 | home-assistant | 0xf07d0
![kép](https://user-images.githubusercontent.com/1550668/112603389-38015180-8e15-11eb-8907-933f5a39e6b5.png) | x | \uE6A1 | home-outline | 0xf06a1
![kép](https://user-images.githubusercontent.com/1550668/112610117-9ed63900-8e1c-11eb-9a2f-658943c320d1.png) | x | \uE2DE | home-variant | 0xf02de
![kép](https://user-images.githubusercontent.com/1550668/112610146-a7c70a80-8e1c-11eb-91b2-6ccbadd372ce.png) | x | \uEBA7 | home-variant-outline | 0xf0ba7
![kép](https://user-images.githubusercontent.com/1550668/112610180-b1e90900-8e1c-11eb-867c-3a4c9b56f133.png) | x | \uECCB | shield-home-outline | 0xf0ccb
![kép](https://user-images.githubusercontent.com/1550668/112603529-6bdc7700-8e15-11eb-86fe-e11e703f8f0d.png) | x | \uE40E | play-pause | 0xf040e
![kép](https://user-images.githubusercontent.com/1550668/112603555-75fe7580-8e15-11eb-91ac-51eb3b3a2c74.png) | x | \uE40A | play | 0xf040a
![kép](https://user-images.githubusercontent.com/1550668/112603579-7eef4700-8e15-11eb-9774-7a5c033c4213.png) | x | \uE3E4 | pause | 0xf03e4
![kép](https://user-images.githubusercontent.com/1550668/112603634-8f072680-8e15-11eb-97b8-f03746b0c5ca.png) | x | \uE4DB | stop | 0xf04db
![kép](https://user-images.githubusercontent.com/1550668/112603660-98908e80-8e15-11eb-9ada-365515c9fa29.png) |  | \uE211 | fast-forward | 0xf0211
![kép](https://user-images.githubusercontent.com/1550668/112603689-a3e3ba00-8e15-11eb-80f9-925e709193d0.png) |  | \uE45F | rewind | 0xf045f
![kép](https://user-images.githubusercontent.com/1550668/112603724-ae05b880-8e15-11eb-93a8-473dc5e1fc4c.png) | x | \uE4AD | skip-next | 0xf04ad
![kép](https://user-images.githubusercontent.com/1550668/112603763-b6f68a00-8e15-11eb-98f6-ce3f58450405.png) | x | \uE4AE | skip-previous | 0xf04ae
![kép](https://user-images.githubusercontent.com/1550668/113571517-d0b67f00-9616-11eb-816f-810a6b55b6d5.png) | x | \uE456 | repeat | 0xf0456
![kép](https://user-images.githubusercontent.com/1550668/113571532-d744f680-9616-11eb-8ed5-26dbc23050fb.png) | x | \uE457 | repeat-off | 0xf0457
![kép](https://user-images.githubusercontent.com/1550668/113571554-df049b00-9616-11eb-9697-c4742e0ffcad.png) | x | \uE458 | repeat-once | 0xf0458
![kép](https://user-images.githubusercontent.com/1550668/113571567-e9bf3000-9616-11eb-816d-e05be9aa0f5b.png) | x | \uE49D | shuffle | 0xf049d
![kép](https://user-images.githubusercontent.com/1550668/113571584-f2176b00-9616-11eb-82f4-7f799e3cbaa6.png) | x | \uE49E | shuffle-disabled | 0xf049e
![kép](https://user-images.githubusercontent.com/1550668/112603885-df7e8400-8e15-11eb-891f-73e9e6de7a35.png) |  | \uE75A | music | 0xf075a
![kép](https://user-images.githubusercontent.com/1550668/112603943-ef966380-8e15-11eb-99f7-e05503f8af8c.png) | x | \uE57E | volume-high | 0xf057e
![kép](https://user-images.githubusercontent.com/1550668/112603974-f7ee9e80-8e15-11eb-8430-03dbd224356f.png) |  | \uE57F | volume-low | 0xf057f
![kép](https://user-images.githubusercontent.com/1550668/112604010-02109d00-8e16-11eb-85e1-cdd691c9e1fb.png) |  | \uE580 | volume-medium | 0xf0580
![kép](https://user-images.githubusercontent.com/1550668/112604058-0b9a0500-8e16-11eb-992b-3785e033f3f7.png) | x | \uE75F | volume-mute | 0xf075f
![kép](https://user-images.githubusercontent.com/1550668/112604093-15bc0380-8e16-11eb-86dc-443a092516d2.png) |  | \uE36C | microphone | 0xf036c
![kép](https://user-images.githubusercontent.com/1550668/112604143-20769880-8e16-11eb-98a6-67dd706e5901.png) |  | \uE36D | microphone-off | 0xf036d
![kép](https://user-images.githubusercontent.com/1550668/112604966-0f7a5700-8e17-11eb-803a-6ce3cf71bd81.png) | x | \uE502 | television | 0xf0502
![kép](https://user-images.githubusercontent.com/1550668/112607635-b6f88900-8e19-11eb-9c7c-340efe542a08.png) |  | \uE439 | radio | 0xf0439
![kép](https://user-images.githubusercontent.com/1550668/112607677-bfe95a80-8e19-11eb-810c-fb0eec8bbb1b.png) | x | \uE4C3 | speaker | 0xf04c3
![kép](https://user-images.githubusercontent.com/1550668/112607733-c972c280-8e19-11eb-9e6b-c2d5c8ae1cee.png) | x | \uE4C4 | speaker-off | 0xf04c4
![kép](https://user-images.githubusercontent.com/1550668/112607775-d2fc2a80-8e19-11eb-9fbd-4a4e0d637d04.png) | x | \uEF5F | monitor-speaker | 0xf0f5f
![kép](https://user-images.githubusercontent.com/1550668/112604928-05585880-8e17-11eb-81c5-62a221626c04.png) | x | \uE62E | tune (settings) | 0xf062e
![kép](https://user-images.githubusercontent.com/1550668/112604635-aabefc80-8e16-11eb-8235-2f9b1fdeca1c.png) |  | \uE379 | monitor | 0xf0379
![kép](https://user-images.githubusercontent.com/1550668/112604739-c7f3cb00-8e16-11eb-9004-f035e0e70c0f.png) |  | \uE322 | laptop | 0xf0322
![kép](https://user-images.githubusercontent.com/1550668/112604767-d17d3300-8e16-11eb-81cc-efacd94dda1d.png) |  | \uE11C | cellphone | 0xf011c
![kép](https://user-images.githubusercontent.com/1550668/112602997-a85ba300-8e14-11eb-9f0a-7d7acd5e9ab6.png) |  | \uE7C0 | desktop-classic | 0xf07c0
![kép](https://user-images.githubusercontent.com/1550668/112604991-199c5580-8e17-11eb-9fa6-2ef85762c361.png) |  | \uE5A9 | wifi | 0xf05a9
![kép](https://user-images.githubusercontent.com/1550668/112609934-6c2c4080-8e1c-11eb-9e82-142c1ae58f0d.png) |  | \uF119 | antenna | 0xf1119
![kép](https://user-images.githubusercontent.com/1550668/112604895-fa9dc380-8e16-11eb-99de-afa9743f9913.png) | x | \uE4A2 | signal | 0xf04a2
![kép](https://user-images.githubusercontent.com/1550668/113571476-bda3af00-9616-11eb-9f52-0d46c8b2e376.png) |  | \uE0AF | bluetooth | 0xf00af
![kép](https://user-images.githubusercontent.com/1550668/113571502-c72d1700-9616-11eb-9779-7536d38f8ece.png) | x | \uE0B0 | bluetooth-audio | 0xf00b0
![kép](https://user-images.githubusercontent.com/1550668/112605026-2325bd80-8e17-11eb-8d24-e2311f203923.png) | x | \uE9A0 | shower-bath | 0xf09a0
![kép](https://user-images.githubusercontent.com/1550668/112605058-2c168f00-8e17-11eb-91ca-efe8c472c220.png) | x | \uE2E3 | bed | 0xf02e3
![kép](https://user-images.githubusercontent.com/1550668/112605096-3769ba80-8e17-11eb-893c-4f8767629e0c.png) | x | \uF2D1 | sleep | 0xf12d1
![kép](https://user-images.githubusercontent.com/1550668/112605143-4486a980-8e17-11eb-819d-2db58b1925b4.png) | x | \uE4B9 | sofa | 0xf04b9
![kép](https://user-images.githubusercontent.com/1550668/112605179-4fd9d500-8e17-11eb-9fd2-4e4146775354.png) | x | \uE5F2 | food-fork-drink | 0xf05f2
![kép](https://user-images.githubusercontent.com/1550668/112605286-6f70fd80-8e17-11eb-91f2-51b679e03a20.png) | x | \uE176 | coffee | 0xf0176
![kép](https://user-images.githubusercontent.com/1550668/112607795-dc859280-8e19-11eb-8485-bc66ad98e663.png) | x | \uEB7C | chef-hat | 0xf0b7c
![kép](https://user-images.githubusercontent.com/1550668/112605529-b101a880-8e17-11eb-9291-8335883361a6.png) | x | \uEA79 | trash-can | 0xf0a79
![kép](https://user-images.githubusercontent.com/1550668/112605222-5b2d0080-8e17-11eb-86d8-3603f6be3c22.png) | x | \uE9AB | toilet | 0xf09ab
![kép](https://user-images.githubusercontent.com/1550668/112605447-9a5b5180-8e17-11eb-8367-0cecf85ad442.png) |  | \uE1F7 | poo | 0xf01f7
![kép](https://user-images.githubusercontent.com/1550668/112605253-654eff00-8e17-11eb-945b-92f4ab41efd0.png) | x | \uE10B | car | 0xf010b
![kép](https://user-images.githubusercontent.com/1550668/112605492-a6dfaa00-8e17-11eb-8733-a0c114a33439.png) | x | \uE606 | pool | 0xf0606
![kép](https://user-images.githubusercontent.com/1550668/112605578-bfe85b00-8e17-11eb-9ce3-7d591c94c9d5.png) | x | \uE50F | thermometer | 0xf050f
![kép](https://user-images.githubusercontent.com/1550668/112605618-cb3b8680-8e17-11eb-901a-cf5ed06b0c42.png) |  | \uF0C2 | thermometer-high | 0xf10c2
![kép](https://user-images.githubusercontent.com/1550668/112605654-d4c4ee80-8e17-11eb-9821-0348eb47e12d.png) |  | \uF0C3 | thermometer-low | 0xf10c3
![kép](https://user-images.githubusercontent.com/1550668/112605697-de4e5680-8e17-11eb-815d-9cb7779ce30b.png) |  | \uF531 | thermometer-off | 0xf1531
![kép](https://user-images.githubusercontent.com/1550668/112605760-eefecc80-8e17-11eb-91f7-81f6580c00af.png) | x | \uE58E | water-percent | 0xf058e
![kép](https://user-images.githubusercontent.com/1550668/112605827-02aa3300-8e18-11eb-9c62-90f78569883c.png) |  | \uE590 | weather-cloudy | 0xf0590
![kép](https://user-images.githubusercontent.com/1550668/112605863-0c339b00-8e18-11eb-9de2-26da56d5d9e1.png) |  | \uE592 | weather-hail | 0xf0592
![kép](https://user-images.githubusercontent.com/1550668/112605916-1786c680-8e18-11eb-8fc3-aff86431ce31.png) |  | \uE596 | weather-pouring | 0xf0596
![kép](https://user-images.githubusercontent.com/1550668/112605957-22415b80-8e18-11eb-91c9-bf5ab9ce509b.png) | x | \uE599 | weather-sunny | 0xf0599
![kép](https://user-images.githubusercontent.com/1550668/112605997-2cfbf080-8e18-11eb-95d9-b317c55f647a.png) |  | \uE595 | weather-partly-cloudy | 0xf0595
![kép](https://user-images.githubusercontent.com/1550668/112606026-35ecc200-8e18-11eb-8bfa-4e3a6c002b92.png) |  | \uE594 | weather-night | 0xf0594
![kép](https://user-images.githubusercontent.com/1550668/112606066-400ec080-8e18-11eb-9f4a-371ae05d33d5.png) |  | \uEF31 | weather-night-partly-cloudy | 0xf0f31
![kép](https://user-images.githubusercontent.com/1550668/112606106-4a30bf00-8e18-11eb-9cbb-b53d46ee02ab.png) |  | \uE591 | weather-fog | 0xf0591
![kép](https://user-images.githubusercontent.com/1550668/112606136-53219080-8e18-11eb-8548-db20cbb356f7.png) |  | \uE59D | weather-windy | 0xf059d
![kép](https://user-images.githubusercontent.com/1550668/112606173-5d438f00-8e18-11eb-86fd-e912601ebbb6.png) | x | \uE717 | snowflake | 0xf0717
![kép](https://user-images.githubusercontent.com/1550668/112606209-66ccf700-8e18-11eb-9ad4-3169bbcba5fe.png) |  | \uE54A | umbrella | 0xf054a
![kép](https://user-images.githubusercontent.com/1550668/112607543-9af4e780-8e19-11eb-9825-c457f99d834b.png) | x | \uE32A | leaf | 0xf032a
![kép](https://user-images.githubusercontent.com/1550668/112607569-a5af7c80-8e19-11eb-9062-d0a9e45367de.png) | x | \uE405 | pine-tree | 0xf0405
![kép](https://user-images.githubusercontent.com/1550668/112608053-2b332c80-8e1a-11eb-946b-73fa5ae9a1d5.png) | x | \uE5F1 | ev-station | 0xf05f1
![kép](https://user-images.githubusercontent.com/1550668/112609960-751d1200-8e1c-11eb-91c6-e91a4cbbff7d.png) | x | \uF40B | lightning-bolt | 0xf140b
![kép](https://user-images.githubusercontent.com/1550668/112605787-f7ef9e00-8e17-11eb-8633-b7511f56b599.png) |  | \uE241 | flash | 0xf0241
![kép](https://user-images.githubusercontent.com/1550668/112607838-ee673580-8e19-11eb-8fb1-8994d9d7b562.png) |  | \uE2D1 | heart | 0xf02d1
![kép](https://user-images.githubusercontent.com/1550668/112607157-3043ac00-8e19-11eb-8384-03cc74def418.png) |  | \uE4CE | star | 0xf04ce
![kép](https://user-images.githubusercontent.com/1550668/112607225-43ef1280-8e19-11eb-9ade-3771c76b21f5.png) |  | \uE831 | shape | 0xf0831
![kép](https://user-images.githubusercontent.com/1550668/113571610-fc396980-9616-11eb-973e-f0c995878b5c.png) | x | \uEE95 | circle-double | 0xf0e95
![kép](https://user-images.githubusercontent.com/1550668/112606251-6fbdc880-8e18-11eb-9baf-dbf838b0ccd1.png) |  | \uE06E | backspace | 0xf006e
![kép](https://user-images.githubusercontent.com/1550668/112606479-b0b5dd00-8e18-11eb-9b78-e2337df013fc.png) | x | \uE64A | human-greeting | 0xf064a
![kép](https://user-images.githubusercontent.com/1550668/112606655-ba3f4500-8e18-11eb-9b1a-efcfe21c49a5.png) | x | \uE004 | account | 0xf0004
![kép](https://user-images.githubusercontent.com/1550668/112606817-c4614380-8e18-11eb-90c0-771bbc16a411.png) |  | \uEBC8 | skull-outline | 0xf0bc8
![kép](https://user-images.githubusercontent.com/1550668/112607191-3c2f6e00-8e19-11eb-99f7-faf4158e1c5a.png) |  | \uE589 | watch | 0xf0589
![kép](https://user-images.githubusercontent.com/1550668/112607604-ae07b780-8e19-11eb-8a01-2b639f3a7284.png) |  | \uE150 | clock-outline | 0xf0150
![kép](https://user-images.githubusercontent.com/1550668/112607270-4f423e00-8e19-11eb-8ba8-44ed2cf20b7e.png) |  | \uF739 | chat-question-outline | 0xf1739
![kép](https://user-images.githubusercontent.com/1550668/112607869-f8893400-8e19-11eb-8e25-e3cd03a99802.png) |  | \uE08E | battery-outline | 0xf008e
![kép](https://user-images.githubusercontent.com/1550668/112607898-0343c900-8e1a-11eb-9623-c6df0283d7ba.png) |  | \uF2A1 | battery-low | 0xf12a1
![kép](https://user-images.githubusercontent.com/1550668/112607945-0c349a80-8e1a-11eb-82b4-bd205d172eba.png) |  | \uF2A2 | battery-medium | 0xf12a2
![kép](https://user-images.githubusercontent.com/1550668/112607986-16ef2f80-8e1a-11eb-98ff-570307067fe3.png) |  | \uF2A3 | battery-high | 0xf12a3
![kép](https://user-images.githubusercontent.com/1550668/112608017-21112e00-8e1a-11eb-9fa3-f2ce3f49550b.png) |  | \uE349 | magnify | 0xf0349
