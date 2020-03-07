# WenPingYu
Using FFMPEG transcode a bmp image that was get from OpenCV and convert it from RGB format to YCbCr 

YUV420P:
The concept of FFMPEG is insert R'G'B to pict->data[0],pict->data[1] and pict->data[0] CR.
		//Y Color
		int index;
		for (int row = 0; row < pict->height; row++)
		{
			for (int col = 0; col < pict->width; col++) 
			{
				double R = (*(pData + row * stepWidth  + col * nChannels  + 2));
				double G = (*(pData + row * stepWidth  + col * nChannels  + 1));
				double B = (*(pData + row * stepWidth  + col * nChannels ));
			
				pict->data[0][row * pict->linesize[0] + col] = 0.257 * R + 0.504 * G + 0.098 * B + 16;
			}
		}
				
		
		// Cb and Cr
		for (int row = 0; row < pict->height / 2; row++)
		{
			for (int col = 0; col < pict->width / 2; col++)
			{
				double R = (*(pData + row * stepWidth * 2 + col * nChannels * 2 + 2));
				double G= (*(pData + row * stepWidth * 2 + col * nChannels * 2 + 1));
				double B = (*(pData + row * stepWidth * 2 + col * nChannels * 2 ));
				double Y = 0.257 * R + 0.504 * G + 0.098 * B + 16;
		
				pict->data[1][row * pict->linesize[1] + col] = -0.148 * R - 0.291 * G + 0.439 * B + 128;
				pict->data[2][row * pict->linesize[2] + col] = 0.439 * R - 0.368 * G - 0.071 * B + 128;
			}
		}

