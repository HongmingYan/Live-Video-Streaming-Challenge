Table of Contents
=================

   * [Architecture]()
   * [SIM ENV]()
   * [Online]() 
   * [ABR]()
   * [Submit]()
   * [Dataset]()
   
# Architecture
* Live-Video-Streaming-Challenge (ACM MM 2019 Grand Challenge)
* ![Image text](https://github.com/NGnetLab/Live-Video-Streaming-Challenge/blob/master/幻灯片1.gif)
* Document description:
     * online.py       --- ```An SDK to call the SIM and ABR ```
     * dataset         --- ```network trace and video trace
     * ABR.py          --- ```your ABR algorithm```
     * fixed_env.py    --- ```SIM code simulates live streaming player download, play, card, skip frame, etc```
     * load_trace.py   --- ```load trace to memory```
# SIM Env
* Info: The emulator simulates the logic function of a live video player，which mainly simulates downloading video frames and video frames playing in different network environments.
![Image text](https://github.com/NGnetLab/Live-Video-Streaming-Challenge/blob/master/frame.png)    
* Input :
      1.Frame trace focuses on the dynamics of analog video sources. See the Dataset for details.
      2.Network trace focuses on the dynamics of the simulated network. See the Dataset for details.
      3.ABR algorithm decision, that is rate and target buffer size
      
* Output: The included indicators are: physical time, current download frame, current play time, client buffer size, and so on.Please see the table below for details.

        |   params           | params description                       |  sample    |
        |--------------------|------------------------------------------|------------|
        | time(s)            | physical time                            |   0.46(s)  |
        | time_interval(s)   | duration in this cycle                   |   0.012(s) |  
        | send_data_size(bit)| The data size downloaded in this cycle   |   14871(b) |
        | frame_time_len(s)  | The time length of the frame currently   |   0.04(s)  |
        | rebuf(s)           | The rebuf time of this cycle             |   0.00(s)  |
        | buffer_size(s)     | The buffer size time length              |   1.26(s)  |
        | play_time_len(s)   | The time length of playing in this cycle |   0.012(s) |
        | end_delay(s)       | Current end-to-to delay                  |   1.31(s)  |
        | cdn_newest_id      | Cdn the newest frame id                  |   85       |
        | download_id        | Download frame id                        |   41       |
        | cdn_has_frame      | cdn cumulative frame info                |   1.31(s)  |
        | decision_flag      | Gop boundary flag or I frame flag        |   False    |
        | buffer_flag        | Whether the player is buffering          |   False    |
        | cdn_rebuf_flag     | Whether the cdn is rebuf                 |   False    |
        | end_of_video       | Whether the end of video                 |   False    |
        
# Online
* Setting
    * video trace setting:     
        
                   13 video_size_file = './video_size_'      #video trace path setting,
                   
    * network trace setting:
    
                   12 TRAIN_TRACES = './train_sim_traces/'   #train trace path setting, 
                   
    * log setting
        * the log is used to debug the code. you can set you log file path:

                   14 LogFile_Path = "./log/"                #log file trace path setting, 
        
        * if you are debugging your code, you can let the DEBUG = True.
        * if you are trainning your model, consider the I/O, advise you let the DEBUG = False
    * plot setting
        * if you want to Debug the code, the Draw = True, the image will let you know all kinds of indicators
        * ![Image text](https://github.com/NGnetLab/LiveStreamingDemo/blob/master/figure_1.png)

        ```python
           if DRAW:
               ax = fig.add_subplot(311)
               plt.ylabel("BIT_RATE")
               plt.ylim(300,1000)
               plt.plot(id_list,bit_rate_record,'-r')
  
               ax = fig.add_subplot(312)
               plt.ylabel("Buffer_size")
               plt.ylim(0,7)
               plt.plot(id_list,buffer_record,'-b')
  
               ax = fig.add_subplot(313)
               plt.ylabel("throughput")
               plt.ylim(0,2500)
               plt.plot(id_list,throughput_record,'-g')
  
               plt.draw()
               plt.pause(0.01)
         ```
# ABR
* The participant should submit your ABR algorithm.
* The code must obey the demo sample.
# Submit
* for detail info, Please vist the submit.
# DataSet
* for detail info, Please vist the Dataset.
