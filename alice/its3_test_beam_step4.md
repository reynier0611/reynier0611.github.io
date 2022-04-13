```
|17:32:00.501|  (STATUS) Welcome to Corryvreckan v2.0+766^gd9ef4209
|17:32:00.524|  (STATUS) Loaded 7 detectors        
|17:32:02.086|  (STATUS) Loaded 26 module instances        
|17:32:02.086|  (STATUS) =================| Initializing modules |==================
|17:32:03.400|  (STATUS) [I:Correlations:ALPIDE_0] Initializing "Correlations:ALPIDE_0"           
|17:32:03.400| (WARNING) [I:Correlations:ALPIDE_0] [further messages suppressed] Correlations module is enabled and will significantly increase the runtime
|17:32:04.738|  (STATUS) [I:AnalysisEfficiency:ALPIDE_3] Initializing "AnalysisEfficiency:ALPIDE_3"Warning in <TH1::TH1>: nbins is <=0 - set to nbins = 1

|17:32:04.920|  (STATUS) ========================| Event loop |========================
|17:32:14.640|  (STATUS) Ev: 1.0k Px: 16.2k Tr: 0.8k (0.815/ev) t = 9.99ms 
|17:32:14.641|  (STATUS) ===================| Finalising modules |===================
|17:32:27.291|  (STATUS) [F:DUTAssociation:ALPIDE_3] In total, 618 clusters are associated to 618 tracks.
|17:32:33.416|  (STATUS) [F:AnalysisEfficiency:ALPIDE_3] Track selection flow:       815
                                                         * rejected by chi2          -212
                                                         * track outside ROI         -0
                                                         * track outside DUT         -51
                                                         * track close to masked px  -0
                                                         * track close to frame edge -0
                                                         * track without an associated cluster on required detector - 0
                                                         Accepted tracks:            552
|17:32:33.418|  (STATUS) [F:AnalysisEfficiency:ALPIDE_3] Total efficiency of detector ALPIDE_3: 96.9203(+0.733317 -0.924227)%, measured with 535/552 matched/total tracks
|17:32:34.793|  (STATUS) Wrote histogram output file to "/local/output/analysis_run98765.root"
|17:32:34.794|  (STATUS) ===============| Wall-clock timing (seconds) |================
|17:32:34.794|  (STATUS)            Metronome               --  0.01711s = 0.017107ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_0  --  0.35682s = 0.356824ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_1  --  0.20559s = 0.205589ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_2  --  0.19694s = 0.196938ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_3  --  0.20107s = 0.201074ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_4  --  0.18954s = 0.189541ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_5  --  0.18841s = 0.188412ms/evt
|17:32:34.795|  (STATUS)    EventLoaderEUDAQ2 :   ALPIDE_6  --  0.18948s = 0.189475ms/evt
|17:32:34.795|  (STATUS)    ClusteringSpatial :   ALPIDE_0  --  0.06531s = 0.065310ms/evt
|17:32:34.795|  (STATUS)    ClusteringSpatial :   ALPIDE_1  --  0.03452s = 0.034521ms/evt
|17:32:34.796|  (STATUS)    ClusteringSpatial :   ALPIDE_2  --  0.03009s = 0.030088ms/evt
|17:32:34.796|  (STATUS)    ClusteringSpatial :   ALPIDE_3  --  0.03949s = 0.039494ms/evt
|17:32:34.796|  (STATUS)    ClusteringSpatial :   ALPIDE_4  --  0.02860s = 0.028596ms/evt
|17:32:34.796|  (STATUS)    ClusteringSpatial :   ALPIDE_5  --  0.02974s = 0.029737ms/evt
|17:32:34.796|  (STATUS)    ClusteringSpatial :   ALPIDE_6  --  0.02883s = 0.028826ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_0  --  0.07372s = 0.073723ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_1  --  0.04836s = 0.048359ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_2  --  0.04602s = 0.046021ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_3  --  0.05543s = 0.055434ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_4  --  0.04509s = 0.045091ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_5  --  0.04618s = 0.046181ms/evt
|17:32:34.796|  (STATUS)         Correlations :   ALPIDE_6  --  0.04604s = 0.046043ms/evt
|17:32:34.796|  (STATUS)           Tracking4D               --  0.47097s = 0.470973ms/evt
|17:32:34.796|  (STATUS)       DUTAssociation :   ALPIDE_3  --  0.03489s = 0.034894ms/evt
|17:32:34.796|  (STATUS)          AnalysisDUT :   ALPIDE_3  --  0.09475s = 0.094751ms/evt
|17:32:34.797|  (STATUS)   AnalysisEfficiency :   ALPIDE_3  --  6.88590s = 6.885899ms/evt
|17:32:34.797|  (STATUS) ==============================================================
```