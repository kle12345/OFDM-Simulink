# OFDM simulation using Simulink
This project was carried out as part of the TC department program, INSA Lyon. The goal of the project is to design an OFDM transmitter and a receiver using Simulink, with the use of pilot symbols, cyclic prefix and a multipath channel.

Constraints:
1, Bandwidth: B = 20 MHz;
2, Environment: In order to introduce multipath channel, we assume that the lastest echo received arrives with a delay of 500 ns (*max delay*) compared to the main path. This correspond to a very dense indoor or outdoor environment;
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
![My Remote Image](https://www.dropbox.com/scl/fi/nkr7e45kbjtcljxscgscf/Transmitter.png?rlkey=dhmurk3edrb0ek5ljpkvbl05i&dl=0)

###  Pilot adding principle using Simulink blocs
![My Remote Image](https://www.dropbox.com/scl/fi/k6gwsu2vimjptqgmru0i6/Pilot-adding.png?rlkey=z9a1ousjv9slmzseozcm6keb2&dl=0)


## Receiver
*First part*
![My Remote Image](https://www.dropbox.com/scl/fi/wqmvleu9apjuokmfkpjf8/Receiver-1.png?rlkey=nb42q7o1g5gqhy62irp1xqqqg&dl=0)
*Second part (Equalization)*
![My Remote Image](https://www.dropbox.com/scl/fi/4q01i2q1pqlk4ahg72bhz/Receiver-2.png?rlkey=sv6wkua9imdqrh1th6quv4l03&dl=0)
*Third part*
![My Remote Image](https://www.dropbox.com/scl/fi/c9c6wt1dapgc8725f3xcl/Receiver-3.png?rlkey=2pixlx6x3aqflnnoaw4nsd7aj&dl=0)


## Channel
A Rayleigh bloc is used for the channel:
![My Remote Image](https://www.dropbox.com/scl/fi/aco2zuhih7t1nzd445se5/Rayleigh-bloc.png?rlkey=ttk9cabsut709l8koajfmdx23&dl=0)

With the configuration below:
![My Remote Image](https://www.dropbox.com/scl/fi/lgia0cip2unrn4551w6zn/Rayleigh-channel.png?rlkey=22gt5fb72fe7df5d8btuhg7rm&dl=0)

The synchronization is carried out in a different project, where we measured the BER with different rates of pilot, IFFT sizes and SNR values.
















