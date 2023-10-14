# OFDM simulation using Simulink
This project was carried out as part of the program of the TC department, Insa Lyon. The goal of the project is to design an OFDM transmitter and a receiver using Simulink, with the use of pilot symbols, cyclic prefix and a multipath channel.

Constraints:
1, Bandwidth: B = 20 MHz
2, Environment: In order to introduce multipath channel, we assume that the lastest echo received arrives with a delay of 500 ns (*max delay*) compared to the main path. This correspond to a very dense indoor or outdoor environment.
3, Maximum Doppler shift: 100 Hz

The transmission being carried out on a multipath channel introducing echoes and delays upon reception, to have a flat fading allowing a constant channel response on a frequency band, the subband width W must respect the following condition: W << 1/*max delay*. For this reason, we chose W = 0.2 MHz.
As a consequence:
Tofdm = 1/W = 5 μs
N = B/W = 100 subbands
Np = N*pilot rate =  25 pilots
Yet the number of samples at the input of the IFFT block must be a multiple of 2, we therefore chose Ntot = 128 and added zeros to the first and last 14 samples of our frame. 
Tb = Tofdm/[2*(N-Np)] = 33 ns
Te = Tofdm/(Npc+Ntot) = 35 ns

The number of cyclic prefix must follow the condition: Npc*Te = *max delay* => Npc = 14 samples

| Number of samples at IFFT block input (Ntot) | 128 | 
| Number of subbands (N) | 100 |
| Subband width (W) | 0.2 MHz  |
| OFDM symbol rate (Tofdm) | 5 μs |
| Bit-rate (Tb) | 33 ns |
| Sample time (Te)| 35 ns |
| Pilot rate | 25% |
| Number of pilots (Np) | 25 |
| Number of cyclic prefix (Npc) | 14 |

The final model is in file Projet_PSC.slx.

## Transmitter
![My Remote Image](https://keep.google.com/u/0/media/v2/17fJ-nr0MzMPeWkl9qpDk-Z2E1uSJr_matWCSkz6YVgEDGqAbYAbxBmoOEelMStg/1Yg5GZZUPRt6Tji3yPuyo9P4BwtSvbh_QDNSms7c6P2_it1UxrNc9QqEvMsuG2g?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)

###  Pilot adding principle using Simulink blocs
![My Remote Image](https://keep.google.com/u/0/media/v2/1MnIbOqQ0GvTcn9oh_X_-LKNnAggSHUOuQNO7PZeh9TVO5CbZ4dXhcLF8Gnvdxpg/11_15NHcg7uQKanIo1cY7SIFXsAXHEop5zSm8R515VUDmzkXEVf1QjUigRdlVlBE?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)


## Receiver
*First part*
![My Remote Image](https://keep.google.com/u/0/media/v2/1K-FQ5P7QcsvnEGcMHQSxYO2IiLtAuqluYGckfbwXu1lszhFghqvKQFZJ6XxrEcw/1P3RLW8XJGkSXI2-vEjE-tFInf2EWvxhEsqyT6uZ6vTqho9PZg3hGKkOBYVX_r0c?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)
*Second part (Equalization)*
![My Remote Image](https://keep.google.com/u/0/media/v2/1e4vaX3xeOYWYjdyN7Q9owXYERNIlTTAyn_LbrOpzFOkHPRveyfG4HOoy3w0w7g/1rvm1FWQOleaiCb9saW2-dSBaSXXfE_jU82qtDQCpJJYZ6xrITvbZQMnAi_RsJQ?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)
*Third part*
![My Remote Image](https://keep.google.com/u/0/media/v2/12KeRql-2yIwMsZpemMdYe1b3cgXcJItAfq0jWTTYDEWdzrmBUVV7cLrxpp0gvg/10VOwyx04WZQqFNAp_V7BOTLaCe7Jk2dyoVvT2or1ohnZ_Eyr3VuRwWHqG9h9fbw?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)


## Channel
A Rayleigh bloc is used for the channel:
![My Remote Image](https://keep.google.com/u/0/media/v2/1UUs_ZbNYJ1hr9XlyEuFoGtB6rIV4g3evtMXPm0YbVzPVR0aFawdEpmEI1M_Z3qM/18woDVdBQeA5BfsAMut1tEzXS3d8kk-ruurMQpGD_D6TbqWicWD9eM2zcokD0gw?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)

With the configuration below:
![My Remote Image](https://keep.google.com/u/0/media/v2/1y5PfyRtRvB7B4mLCKAvxY6xwz0pTTATO_P6LMhjYUha6K2bPdiXVF_NTvl8_k30/1A9cVmGSACm78P0qY-L-FiSdepTjgb710Kl5JbCTUiESC5gl2gr7myXsD9e7VMA?sz=512&accept=image%2Fgif%2Cimage%2Fjpeg%2Cimage%2Fjpg%2Cimage%2Fpng%2Cimage%2Fwebp)

The synchronization is carried out in a different project, where we measured the BER with different rates of pilot, IFFT sizes and SNR values.
















