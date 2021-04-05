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

Compile the firnware with platformio as usual, and flash it OTA to your device. To display the desired icon, simply use your custom font size (in our example 26): `p4b1.text_font=26`, and in the `jsonl` command specify the escaped, _shifted down_ character code from the table below:

Icon  | Suggested<br>for default  | Character code<br>shifted down by EFFE0  | Original MDI Character code  | Description
--  | --  | --  | -- | --
![kép](https://user-images.githubusercontent.com/1550668/112601640-f96a9780-8e12-11eb-8b5e-9e139cdce82c.png)  | x  | \u0065  | 0xf0045  | arrow down
![kép](https://user-images.githubusercontent.com/1550668/112602206-ab09c880-8e13-11eb-9a01-ac8ae774375e.png)  | x  | \u007d  | 0xf005d  | arrow up
![kép](https://user-images.githubusercontent.com/1550668/112602286-c1b01f80-8e13-11eb-86c1-151297c42082.png)  | x  | \u006d  | 0xf004d  | arrow left
![kép](https://user-images.githubusercontent.com/1550668/112602326-cecd0e80-8e13-11eb-84a4-89794d128165.png)  | x  | \u0074  | 0xf0054  | arrow right
![kép](https://user-images.githubusercontent.com/1550668/112603048-bc9fa000-8e14-11eb-92fc-5f9894abffa1.png)  |   | \u06e3  | 0xf06c3  | arrow-up-box
![kép](https://user-images.githubusercontent.com/1550668/112609991-7f3f1080-8e1c-11eb-90f6-fa824f5b4a4b.png)  |   | \u06e0  | 0xf06c0  | arrow-down-box
![kép](https://user-images.githubusercontent.com/1550668/112603107-d04b0680-8e14-11eb-964a-a3392fddf94c.png)  |   | \u06e1  | 0xf06c1  | arrow-left-box
![kép](https://user-images.githubusercontent.com/1550668/112603142-de992280-8e14-11eb-9bac-62dd62137aa1.png)  |   | \u06e2  | 0xf06c2  | arrow-right-box
![kép](https://user-images.githubusercontent.com/1550668/112602394-e5736580-8e13-11eb-98af-59081b367f7a.png)  |   | \u0160  | 0xf0140  | chevron down
![kép](https://user-images.githubusercontent.com/1550668/112602450-fd4ae980-8e13-11eb-9651-606014d168a3.png)  |   | \u0161  | 0xf0141  | chevron left
![kép](https://user-images.githubusercontent.com/1550668/112602478-0936ab80-8e14-11eb-9abe-a18becdc1731.png)  |   | \u0162  | 0xf0142  | chevron right
![kép](https://user-images.githubusercontent.com/1550668/112602516-1358aa00-8e14-11eb-83d3-179428948db5.png)  |   | \u0163  | 0xf0143  | chevron up
![kép](https://user-images.githubusercontent.com/1550668/112603414-42bbe680-8e15-11eb-9217-3b846d89d9df.png)  |   | \u037d  | 0xf035d  | menu-down
![kép](https://user-images.githubusercontent.com/1550668/112603445-4e0f1200-8e15-11eb-8b1d-b971da582020.png)  |   | \u037e  | 0xf035e  | menu-left
![kép](https://user-images.githubusercontent.com/1550668/112603469-58311080-8e15-11eb-8e1e-b2e11bb6040a.png)  |   | \u037f  | 0xf035f  | menu-right
![kép](https://user-images.githubusercontent.com/1550668/112603495-63843c00-8e15-11eb-8434-3a0925359dbf.png)  |   | \u0380  | 0xf0360  | menu-up
![kép](https://user-images.githubusercontent.com/1550668/112604191-2a989700-8e16-11eb-81fd-6b485910d68e.png)  | x  | \u0435  | 0xf0415  | plus
![kép](https://user-images.githubusercontent.com/1550668/112604245-33896880-8e16-11eb-843f-f4d20f5d7686.png)  | x  | \u0394  | 0xf0374  | minus
![kép](https://user-images.githubusercontent.com/1550668/112607306-5b2e0000-8e19-11eb-83d3-cac0094e24b1.png)  |   | \u0437  | 0xf0417  | plus-circle
![kép](https://user-images.githubusercontent.com/1550668/112607391-7436b100-8e19-11eb-87b1-fbf7d9aabcc2.png)  |   | \u0396  | 0xf0376  | minus-circle
![kép](https://user-images.githubusercontent.com/1550668/112607352-6719c200-8e19-11eb-90b9-297fc9166dd6.png)  |   | \u0436  | 0xf0416  | plus-box
![kép](https://user-images.githubusercontent.com/1550668/112607434-7f89dc80-8e19-11eb-8eeb-4f1d18daac4f.png)  |   | \u0395  | 0xf0375  | minus-box
![kép](https://user-images.githubusercontent.com/1550668/112606281-79473080-8e18-11eb-9434-628d816637ba.png)  |   | \u014c  | 0xf012c  | check
![kép](https://user-images.githubusercontent.com/1550668/112606311-82d09880-8e18-11eb-99b9-911ff7173432.png)  |   | \u0601  | 0xf05e1  | check-circle-outline
![kép](https://user-images.githubusercontent.com/1550668/112606342-8d8b2d80-8e18-11eb-898a-c512d721ccf6.png)  |   | \u0c72  | 0xf0c52  | check-box-outline
![kép](https://user-images.githubusercontent.com/1550668/112606364-95e36880-8e18-11eb-9172-a019ec848055.png)  |   | \u04b3  | 0xf0493  | cog
![kép](https://user-images.githubusercontent.com/1550668/112606395-a09dfd80-8e18-11eb-9648-ed565d61ede6.png)  |   | \u066e  | 0xf064e  | info
![kép](https://user-images.githubusercontent.com/1550668/112602593-2e2b1e80-8e14-11eb-9a46-b6beaf1ac37d.png)  | x  | \u0355  | 0xf0335  | lightbulb
![kép](https://user-images.githubusercontent.com/1550668/112602634-3aaf7700-8e14-11eb-802e-81abd2af1a8a.png)  | x  | \u0356  | 0xf0336  | lightbulb-outline
![kép](https://user-images.githubusercontent.com/1550668/112608099-35552b00-8e1a-11eb-92a6-315ea28c5b01.png)  | x  | \u0708  | 0xf06e8  | lightbulb-on
![kép](https://user-images.githubusercontent.com/1550668/112608123-3d14cf80-8e1a-11eb-8184-07d377d7941f.png)  | x  | \u0709  | 0xf06e9  | lightbulb-on-outline
![kép](https://user-images.githubusercontent.com/1550668/112604790-db069b00-8e16-11eb-9416-03a844f45554.png)  | x  | \u06c5  | 0xf06a5  | power-plug
![kép](https://user-images.githubusercontent.com/1550668/112604833-e5c13000-8e16-11eb-93ef-526ab3d76df3.png)  | x  | \u06c6  | 0xf06a6  | power-plug-off
![kép](https://user-images.githubusercontent.com/1550668/112604861-ef4a9800-8e16-11eb-891d-0ac1be573a7c.png)  | x  | \u0445  | 0xf0425  | power
![kép](https://user-images.githubusercontent.com/1550668/112602682-49962980-8e14-11eb-8f78-ddabc6e616cb.png)  | x  | \u0458  | 0xf0438  | heater-on
![kép](https://user-images.githubusercontent.com/1550668/112602722-53b82800-8e14-11eb-844b-dc1217efc0cd.png)  | x  | \u0af7  | 0xf0ad7  | heater
![kép](https://user-images.githubusercontent.com/1550668/112602750-5dda2680-8e14-11eb-86dd-4c9672c9a345.png)  | x  | \u0af8  | 0xf0ad8  | heater-off
![kép](https://user-images.githubusercontent.com/1550668/112604287-3dab6700-8e16-11eb-9d13-e0b9a6012ebf.png)  | x  | \u083b  | 0xf081b  | door-closed
![kép](https://user-images.githubusercontent.com/1550668/112604313-469c3880-8e16-11eb-9715-0afabb5b551c.png)  | x  | \u10cf  | 0xf10af  | door-closed-lock
![kép](https://user-images.githubusercontent.com/1550668/112604349-5156cd80-8e16-11eb-9dab-05430fadb59e.png)  | x  | \u083c  | 0xf081c  | door-open
![kép](https://user-images.githubusercontent.com/1550668/112604526-895e1080-8e16-11eb-8c09-2c7b4290c955.png)  |   | \u0541  | 0xf0521  | toggle-switch
![kép](https://user-images.githubusercontent.com/1550668/112604555-93800f00-8e16-11eb-8087-2abf445d6775.png)  |   | \u0542  | 0xf0522  | toggle-switch-off
![kép](https://user-images.githubusercontent.com/1550668/112604595-9ed33a80-8e16-11eb-8c88-f1ed11972e83.png)  | x  | \u00ba  | 0xf009a  | bell
![kép](https://user-images.githubusercontent.com/1550668/112603223-fec8e180-8e14-11eb-93dd-769c84d478b0.png)  | x  | \u113c  | 0xf111c  | window shutter closed
![kép](https://user-images.githubusercontent.com/1550668/112603260-0ab4a380-8e15-11eb-85c5-b1559d985f5d.png)  | x  | \u113d  | 0xf111d  | window shutter warning
![kép](https://user-images.githubusercontent.com/1550668/112603287-156f3880-8e15-11eb-9248-239b45f2c91d.png)  | x  | \u113e  | 0xf111e  | window shutter open
![kép](https://user-images.githubusercontent.com/1550668/112603171-ea84e480-8e14-11eb-9224-47e584a87d1c.png)  |   | \u06f9  | 0xf06d9  | garage closed
![kép](https://user-images.githubusercontent.com/1550668/112603197-f40e4c80-8e14-11eb-8304-4e3b5595433f.png)  |   | \u06fa  | 0xf06da  | garage open
![kép](https://user-images.githubusercontent.com/1550668/112610031-89f9a580-8e1c-11eb-92ea-ce7caa099650.png)  | x  | \u12f3  | 0xf12d3  | garage-variant
![kép](https://user-images.githubusercontent.com/1550668/112610076-94b43a80-8e1c-11eb-9832-c48d50d16372.png)  | x  | \u12f4  | 0xf12d4  | garage-open-variant
![kép](https://user-images.githubusercontent.com/1550668/112604467-75b2aa00-8e16-11eb-89c4-51cfb5417264.png)  |   | \u035e  | 0xf033e  | lock
![kép](https://user-images.githubusercontent.com/1550668/112604496-7fd4a880-8e16-11eb-8d7a-f46cf7e5fd1a.png)  |   | \u0fe6  | 0xf0fc6  | lock-open-variant
![kép](https://user-images.githubusercontent.com/1550668/112605399-8dd6f900-8e17-11eb-9460-bbff85df74c7.png)  |   | \u032b  | 0xf030b  | key-variant
![kép](https://user-images.githubusercontent.com/1550668/112604381-5d428f80-8e16-11eb-8004-b62016ecb41c.png)  |   | \u0228  | 0xf0208  | eye
![kép](https://user-images.githubusercontent.com/1550668/112604430-6a5f7e80-8e16-11eb-8d80-22a6c8711726.png)  |   | \u0229  | 0xf0209  | eye-off
![kép](https://user-images.githubusercontent.com/1550668/112607816-e60efa80-8e19-11eb-9d04-f5a34578eb87.png)  | x  | \u0e66  | 0xf0e46  | hand-left
![kép](https://user-images.githubusercontent.com/1550668/112609893-633b6f00-8e1c-11eb-8f3e-91cf0eaea5bf.png)  | x  | \u0046  | 0xf0026  | alert
![kép](https://user-images.githubusercontent.com/1550668/112605323-7861cf00-8e17-11eb-9560-42dbe8608504.png)  | x  | \u02fc  | 0xf02dc  | home
![kép](https://user-images.githubusercontent.com/1550668/112605354-8283cd80-8e17-11eb-97d7-1de87e58d188.png)  | x  | \u07f0  | 0xf07d0  | home-assistant
![kép](https://user-images.githubusercontent.com/1550668/112603389-38015180-8e15-11eb-8907-933f5a39e6b5.png)  | x  | \u06c1  | 0xf06a1  | home-outline
![kép](https://user-images.githubusercontent.com/1550668/112610117-9ed63900-8e1c-11eb-9a2f-658943c320d1.png)  | x  | \u02fe  | 0xf02de  | home-variant
![kép](https://user-images.githubusercontent.com/1550668/112610146-a7c70a80-8e1c-11eb-91b2-6ccbadd372ce.png)  | x  | \u0bc7  | 0xf0ba7  | home-variant-outline
![kép](https://user-images.githubusercontent.com/1550668/112610180-b1e90900-8e1c-11eb-867c-3a4c9b56f133.png)  | x  | \u0ceb  | 0xf0ccb  | shield-home-outline
![kép](https://user-images.githubusercontent.com/1550668/112603529-6bdc7700-8e15-11eb-86fe-e11e703f8f0d.png)  | x  | \u042e  | 0xf040e  | play-pause
![kép](https://user-images.githubusercontent.com/1550668/112603555-75fe7580-8e15-11eb-91ac-51eb3b3a2c74.png)  | x  | \u042a  | 0xf040a  | play
![kép](https://user-images.githubusercontent.com/1550668/112603579-7eef4700-8e15-11eb-9774-7a5c033c4213.png)  | x  | \u0404  | 0xf03e4  | pause
![kép](https://user-images.githubusercontent.com/1550668/112603634-8f072680-8e15-11eb-97b8-f03746b0c5ca.png)  | x  | \u04fb  | 0xf04db  | stop
![kép](https://user-images.githubusercontent.com/1550668/112603660-98908e80-8e15-11eb-9ada-365515c9fa29.png)  |   | \u0231  | 0xf0211  | fast-forward
![kép](https://user-images.githubusercontent.com/1550668/112603689-a3e3ba00-8e15-11eb-80f9-925e709193d0.png)  |   | \u047f  | 0xf045f  | rewind
![kép](https://user-images.githubusercontent.com/1550668/112603724-ae05b880-8e15-11eb-93a8-473dc5e1fc4c.png)  | x  | \u04cd  | 0xf04ad  | skip-next
![kép](https://user-images.githubusercontent.com/1550668/112603763-b6f68a00-8e15-11eb-98f6-ce3f58450405.png)  | x  | \u04ce  | 0xf04ae  | skip-previous
![kép](https://user-images.githubusercontent.com/1550668/113571517-d0b67f00-9616-11eb-816f-810a6b55b6d5.png)  | x  | \u0476  | 0xf0456  | repeat
![kép](https://user-images.githubusercontent.com/1550668/113571532-d744f680-9616-11eb-8ed5-26dbc23050fb.png)  | x  | \u0477  | 0xf0457  | repeat-off
![kép](https://user-images.githubusercontent.com/1550668/113571554-df049b00-9616-11eb-9697-c4742e0ffcad.png)  | x  | \u0478  | 0xf0458  | repeat-once
![kép](https://user-images.githubusercontent.com/1550668/113571567-e9bf3000-9616-11eb-816d-e05be9aa0f5b.png)  | x  | \u04BD  | 0xf049d  | shuffle
![kép](https://user-images.githubusercontent.com/1550668/113571584-f2176b00-9616-11eb-82f4-7f799e3cbaa6.png)  | x  | \u04BE  | 0xf049e  | shuffle-disabled
![kép](https://user-images.githubusercontent.com/1550668/112603885-df7e8400-8e15-11eb-891f-73e9e6de7a35.png)  |   | \u077a  | 0xf075a  | music
![kép](https://user-images.githubusercontent.com/1550668/112603943-ef966380-8e15-11eb-99f7-e05503f8af8c.png)  | x  | \u059e  | 0xf057e  | volume-high
![kép](https://user-images.githubusercontent.com/1550668/112603974-f7ee9e80-8e15-11eb-8430-03dbd224356f.png)  |   | \u059f  | 0xf057f  | volume-low
![kép](https://user-images.githubusercontent.com/1550668/112604010-02109d00-8e16-11eb-85e1-cdd691c9e1fb.png)  |   | \u05a0  | 0xf0580  | volume-medium
![kép](https://user-images.githubusercontent.com/1550668/112604058-0b9a0500-8e16-11eb-992b-3785e033f3f7.png)  | x  | \u077f  | 0xf075f  | volume-mute
![kép](https://user-images.githubusercontent.com/1550668/112604093-15bc0380-8e16-11eb-86dc-443a092516d2.png)  |   | \u038c  | 0xf036c  | microphone
![kép](https://user-images.githubusercontent.com/1550668/112604143-20769880-8e16-11eb-98a6-67dd706e5901.png)  |   | \u038d  | 0xf036d  | microphone-off
![kép](https://user-images.githubusercontent.com/1550668/112604966-0f7a5700-8e17-11eb-803a-6ce3cf71bd81.png)  | x  | \u0522  | 0xf0502  | television
![kép](https://user-images.githubusercontent.com/1550668/112607635-b6f88900-8e19-11eb-9c7c-340efe542a08.png)  |   | \u0459  | 0xf0439  | radio
![kép](https://user-images.githubusercontent.com/1550668/112607677-bfe95a80-8e19-11eb-810c-fb0eec8bbb1b.png)  | x  | \u04e3  | 0xf04c3  | speaker
![kép](https://user-images.githubusercontent.com/1550668/112607733-c972c280-8e19-11eb-9e6b-c2d5c8ae1cee.png)  | x  | \u04e4  | 0xf04c4  | speaker-off
![kép](https://user-images.githubusercontent.com/1550668/112607775-d2fc2a80-8e19-11eb-9fbd-4a4e0d637d04.png)  | x  | \u0f7f  | 0xf0f5f  | monitor-speaker
![kép](https://user-images.githubusercontent.com/1550668/112604928-05585880-8e17-11eb-81c5-62a221626c04.png)  | x  | \u064e  | 0xf062e  | tune (settings)
![kép](https://user-images.githubusercontent.com/1550668/112604635-aabefc80-8e16-11eb-8235-2f9b1fdeca1c.png)  |   | \u0399  | 0xf0379  | monitor
![kép](https://user-images.githubusercontent.com/1550668/112604739-c7f3cb00-8e16-11eb-9004-f035e0e70c0f.png)  |   | \u0342  | 0xf0322  | laptop
![kép](https://user-images.githubusercontent.com/1550668/112604767-d17d3300-8e16-11eb-81cc-efacd94dda1d.png)  |   | \u013c  | 0xf011c  | cellphone
![kép](https://user-images.githubusercontent.com/1550668/112602997-a85ba300-8e14-11eb-9f0a-7d7acd5e9ab6.png)  |   | \u07e0  | 0xf07c0  | desktop-classic
![kép](https://user-images.githubusercontent.com/1550668/112604991-199c5580-8e17-11eb-9fa6-2ef85762c361.png)  | x  | \u05c9  | 0xf05a9  | wifi
![kép](https://user-images.githubusercontent.com/1550668/112609934-6c2c4080-8e1c-11eb-9e82-142c1ae58f0d.png)  | x  | \u1139  | 0xf1119  | antenna
![kép](https://user-images.githubusercontent.com/1550668/112604895-fa9dc380-8e16-11eb-99de-afa9743f9913.png)  | x  | \u04c2  | 0xf04a2  | signal
![kép](https://user-images.githubusercontent.com/1550668/113571476-bda3af00-9616-11eb-9f52-0d46c8b2e376.png)  |   | \u00CF  | 0xf00af  | bluetooth
![kép](https://user-images.githubusercontent.com/1550668/113571502-c72d1700-9616-11eb-9779-7536d38f8ece.png)  | x  | \u00D0  | 0xf00b0  | bluetooth-audio
![kép](https://user-images.githubusercontent.com/1550668/112605026-2325bd80-8e17-11eb-8d24-e2311f203923.png)  | x  | \u09c0  | 0xf09a0  | shower-bath
![kép](https://user-images.githubusercontent.com/1550668/112605058-2c168f00-8e17-11eb-91ca-efe8c472c220.png)  | x  | \u0303  | 0xf02e3  | bed
![kép](https://user-images.githubusercontent.com/1550668/112605096-3769ba80-8e17-11eb-893c-4f8767629e0c.png)  | x  | \u12f1  | 0xf12d1  | sleep
![kép](https://user-images.githubusercontent.com/1550668/112605143-4486a980-8e17-11eb-819d-2db58b1925b4.png)  | x  | \u04d9  | 0xf04b9  | sofa
![kép](https://user-images.githubusercontent.com/1550668/112605179-4fd9d500-8e17-11eb-9fd2-4e4146775354.png)  | x  | \u0612  | 0xf05f2  | food-fork-drink
![kép](https://user-images.githubusercontent.com/1550668/112605286-6f70fd80-8e17-11eb-91f2-51b679e03a20.png)  | x  | \u0196  | 0xf0176  | coffee
![kép](https://user-images.githubusercontent.com/1550668/112607795-dc859280-8e19-11eb-8485-bc66ad98e663.png)  | x  | \u0b9c  | 0xf0b7c  | chef-hat
![kép](https://user-images.githubusercontent.com/1550668/112605529-b101a880-8e17-11eb-9291-8335883361a6.png)  | x  | \u0a99  | 0xf0a79  | trash-can
![kép](https://user-images.githubusercontent.com/1550668/112605222-5b2d0080-8e17-11eb-86d8-3603f6be3c22.png)  | x  | \u09cb  | 0xf09ab  | toilet
![kép](https://user-images.githubusercontent.com/1550668/112605447-9a5b5180-8e17-11eb-8367-0cecf85ad442.png)  |   | \u0217  | 0xf01f7  | poo
![kép](https://user-images.githubusercontent.com/1550668/112605253-654eff00-8e17-11eb-945b-92f4ab41efd0.png)  | x  | \u012b  | 0xf010b  | car
![kép](https://user-images.githubusercontent.com/1550668/112605492-a6dfaa00-8e17-11eb-8733-a0c114a33439.png)  | x  | \u0626  | 0xf0606  | pool
![kép](https://user-images.githubusercontent.com/1550668/112605578-bfe85b00-8e17-11eb-9ce3-7d591c94c9d5.png)  | x  | \u052f  | 0xf050f  | thermometer
![kép](https://user-images.githubusercontent.com/1550668/112605618-cb3b8680-8e17-11eb-901a-cf5ed06b0c42.png)  |   | \u10e2  | 0xf10c2  | thermometer-high
![kép](https://user-images.githubusercontent.com/1550668/112605654-d4c4ee80-8e17-11eb-9821-0348eb47e12d.png)  |   | \u10e3  | 0xf10c3  | thermometer-low
![kép](https://user-images.githubusercontent.com/1550668/112605697-de4e5680-8e17-11eb-815d-9cb7779ce30b.png)  |   | \u1551  | 0xf1531  | thermometer-off
![kép](https://user-images.githubusercontent.com/1550668/112605760-eefecc80-8e17-11eb-91f7-81f6580c00af.png)  | x  | \u05ae  | 0xf058e  | water-percent
![kép](https://user-images.githubusercontent.com/1550668/112605827-02aa3300-8e18-11eb-9c62-90f78569883c.png)  |   | \u05b0  | 0xf0590  | weather-cloudy
![kép](https://user-images.githubusercontent.com/1550668/112605863-0c339b00-8e18-11eb-9de2-26da56d5d9e1.png)  |   | \u05b2  | 0xf0592  | weather-hail
![kép](https://user-images.githubusercontent.com/1550668/112605916-1786c680-8e18-11eb-8fc3-aff86431ce31.png)  |   | \u05b6  | 0xf0596  | weather-pouring
![kép](https://user-images.githubusercontent.com/1550668/112605957-22415b80-8e18-11eb-91c9-bf5ab9ce509b.png)  | x  | \u05b9  | 0xf0599  | weather-sunny
![kép](https://user-images.githubusercontent.com/1550668/112605997-2cfbf080-8e18-11eb-95d9-b317c55f647a.png)  |   | \u05b5  | 0xf0595  | weather-partly-cloudy
![kép](https://user-images.githubusercontent.com/1550668/112606026-35ecc200-8e18-11eb-8bfa-4e3a6c002b92.png)  |   | \u05b4  | 0xf0594  | weather-night
![kép](https://user-images.githubusercontent.com/1550668/112606066-400ec080-8e18-11eb-9f4a-371ae05d33d5.png)  |   | \u0f51  | 0xf0f31  | weather-night-partly-cloudy
![kép](https://user-images.githubusercontent.com/1550668/112606106-4a30bf00-8e18-11eb-9cbb-b53d46ee02ab.png)  |   | \u05b1  | 0xf0591  | weather-fog
![kép](https://user-images.githubusercontent.com/1550668/112606136-53219080-8e18-11eb-8548-db20cbb356f7.png)  |   | \u05bd  | 0xf059d  | weather-windy
![kép](https://user-images.githubusercontent.com/1550668/112606173-5d438f00-8e18-11eb-86fd-e912601ebbb6.png)  | x  | \u0737  | 0xf0717  | snowflake
![kép](https://user-images.githubusercontent.com/1550668/112606209-66ccf700-8e18-11eb-9ad4-3169bbcba5fe.png)  |   | \u056a  | 0xf054a  | umbrella
![kép](https://user-images.githubusercontent.com/1550668/112607543-9af4e780-8e19-11eb-9825-c457f99d834b.png)  | x  | \u034a  | 0xf032a  | leaf
![kép](https://user-images.githubusercontent.com/1550668/112607569-a5af7c80-8e19-11eb-9062-d0a9e45367de.png)  | x  | \u0425  | 0xf0405  | pine-tree
![kép](https://user-images.githubusercontent.com/1550668/112608053-2b332c80-8e1a-11eb-946b-73fa5ae9a1d5.png)  | x  | \u0611  | 0xf05f1  | ev-station
![kép](https://user-images.githubusercontent.com/1550668/112609960-751d1200-8e1c-11eb-91c6-e91a4cbbff7d.png)  | x  | \u142b  | 0xf140b  | lightning-bolt
![kép](https://user-images.githubusercontent.com/1550668/112605787-f7ef9e00-8e17-11eb-8633-b7511f56b599.png)  |   | \u0261  | 0xf0241  | flash
![kép](https://user-images.githubusercontent.com/1550668/112607838-ee673580-8e19-11eb-8fb1-8994d9d7b562.png)  |   | \u02f1  | 0xf02d1  | heart
![kép](https://user-images.githubusercontent.com/1550668/112607157-3043ac00-8e19-11eb-8384-03cc74def418.png)  |   | \u04ee  | 0xf04ce  | star
![kép](https://user-images.githubusercontent.com/1550668/112607225-43ef1280-8e19-11eb-9ade-3771c76b21f5.png)  |   | \u0851  | 0xf0831  | shape
![kép](https://user-images.githubusercontent.com/1550668/113571610-fc396980-9616-11eb-973e-f0c995878b5c.png)  | x  | \u0EB5  | 0xf0e95  | circle-double
![kép](https://user-images.githubusercontent.com/1550668/112606251-6fbdc880-8e18-11eb-9baf-dbf838b0ccd1.png)  |   | \u008e  | 0xf006e  | backspace
![kép](https://user-images.githubusercontent.com/1550668/112606479-b0b5dd00-8e18-11eb-9b78-e2337df013fc.png)  | x  | \u066a  | 0xf064a  | human-greeting
![kép](https://user-images.githubusercontent.com/1550668/112606655-ba3f4500-8e18-11eb-9b1a-efcfe21c49a5.png)  | x  | \u0024  | 0xf0004  | account
![kép](https://user-images.githubusercontent.com/1550668/112606817-c4614380-8e18-11eb-90c0-771bbc16a411.png)  |   | \u0be8  | 0xf0bc8  | skull-outline
![kép](https://user-images.githubusercontent.com/1550668/112607191-3c2f6e00-8e19-11eb-99f7-faf4158e1c5a.png)  |   | \u05a9  | 0xf0589  | watch
![kép](https://user-images.githubusercontent.com/1550668/112607604-ae07b780-8e19-11eb-8a01-2b639f3a7284.png)  |   | \u0170  | 0xf0150  | clock-outline
![kép](https://user-images.githubusercontent.com/1550668/112607270-4f423e00-8e19-11eb-8ba8-44ed2cf20b7e.png)  |   | \u1759  | 0xf1739  | chat-question-outline
![kép](https://user-images.githubusercontent.com/1550668/112607869-f8893400-8e19-11eb-8e25-e3cd03a99802.png)  |   | \u00ae  | 0xf008e  | battery-outline
![kép](https://user-images.githubusercontent.com/1550668/112607898-0343c900-8e1a-11eb-9623-c6df0283d7ba.png)  |   | \u12c1  | 0xf12a1  | battery-low
![kép](https://user-images.githubusercontent.com/1550668/112607945-0c349a80-8e1a-11eb-82b4-bd205d172eba.png)  |   | \u12c2  | 0xf12a2  | battery-medium
![kép](https://user-images.githubusercontent.com/1550668/112607986-16ef2f80-8e1a-11eb-98ff-570307067fe3.png)  |   | \u12c3  | 0xf12a3  | battery-high
![kép](https://user-images.githubusercontent.com/1550668/112608017-21112e00-8e1a-11eb-9fa3-f2ce3f49550b.png)  |   | \u0369  | 0xf0349  | magnify
