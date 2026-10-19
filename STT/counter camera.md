23681-16984 = 6697 16 Shift 3
16984-11640 = 5344 16 Shift 1

ffmpeg -i 2.mp4 \
  -map 0:v:0 -map '0:a:0?' \
  -c:v libx264 -preset medium -crf 20 \
  -pix_fmt yuv420p \
  -tag:v avc1 \
  -movflags +faststart \
  -c:a aac -b:a 128k \
  output_roboflow.mp4