## Download Media file.

Get a media file from youtube test media. 
https://storage.googleapis.com/ytlr-cert.appspot.com/test-materials/media/manual/mtm/spherical_h264_720p_progressive.mp4

## Converting it to VP9 content.
The downloaded content is of h264 and aac codec. We shall convert it to vp9, opus codec using ffmpeg.

		ffmpeg -i spherical_h264_720p_progressive.mp4 \
		  -strict -2 -c:a opus \
		  -vf "scale=-2:360" \
		  -c:v libvpx-vp9 -profile:v 0 \
		  -keyint_min 72 -g 72 \
		  -tile-columns 4 -frame-parallel 1 -speed 1 \
		  -auto-alt-ref 1 -lag-in-frames 25 \
		  -b:v 300k \
		  -y vp9_spherical_h264_360_progressive.mp4


## Converting it to a CBCS content.

We create the CBCS content using shaka-packager. The packager comes in a docker. We can run the docker using the below command. 
		docker run -v /Users/ksomas586/work/embedded/streams/:/media/ -it --rm google/shaka-packager
		
Note: 
/Users/ksomas586/work/embedded/streams is the path in the host system where  vp9_spherical_h264_360_progressive.mp4 is present.

Once inside the docker we can run the below command to create the cbcs content. It uses test key for encryption.

		packager \
		  in=/media/vp9_3spherical_h264_360_progressive.mp4,stream=audio,output=/media/sph_audio.mp4 \
		  in=/media/vp9_3spherical_h264_360_progressive.mp4,stream=video,output=/media/sph_video.mp4 \
		  --protection_scheme cbcs \
		  --enable_widevine_encryption \
		  --key_server_url https://license.uat.widevine.com/cenc/getcontentkey/widevine_test \
		  --content_id 7465737420636f6e74656e74206964 \
		  --signer widevine_test \
		  --aes_signing_key 1ae8ccd0e7985cc0b6203a55855a1034afc252980e970ca90e5202689f947ab9 \
		  --aes_signing_iv d58ce954203b7c9a9a9d467f59839249 \
		  --mpd_output /media/sphere_vp9.mpd
		
Once the command is complete we can exit the docker the created files will be present in the host directory.

## Hosting the app and the asset

Please untar the attached app [dash-player.tar.gz](https://github.com/Karthick-Somasundaresan/Documentation/files/7882283/dash-player.tar.gz)
 (dash-player.html) and host it in any webserver. (here we have used node's http-server)
The created asset should be placed inside the webserver along with the app.


## Playing the content on RPI3
  * In ThunderUI enable Coblat plugin.
  * In the Cobalt plugin page, in the Custom URL, provide the app URL along with the asset location as the query parameter

Below is an example on how to provide it.

	http://10.0.0.3:8080/dash-player/dash-player.html?manifest_url=/mpd/spherical_vp9/sphere_vp9.mpd
