# FishingForFishermen

The background for the contest description from Topcoder.

###Background

NASA wishes to identify whether a vessel is fishing or not based on AIS broadcast reports and contextual data.

###Objective

Create an algorithm to effectively identify if a vessel is fishing based on observable behavior and any additional data such as weather, known fishing grounds, etc. regardless of vessel type or declared purpose.

Your algorithm shall utilize:

AIS positional data
Other data from openly accessible data sources that can be used to determine fishing behavior
Your algorithm should then detect vessels that match the profile of behaviors of vessels engaged in fishing. You must identify whether each vessel is fishing or not at each point in time specified in the data set.

###Data Description

The data set is provided in as a series of AIS messages in NMEA format, each message having one appended field indicating, in Unix epoch time format, the "time of fix" (the time at which each AIS broadcast was received). Some messages may contain duplicates or almost duplicates in the data.

Example AIS messages with the appended Time of Fix:

    "!AIVDM,1,1,,A,15NVOL?002o5KFRJ3Rh@0:;p0000,0*73",1439479221
    "!AIVDM,1,1,,A,1EOP=l7018o6lGPJ>owGtFD>0>@<,0*21",1439698812
    "!AIVDM,1,1,,B,BE2P9a@15eib9RVWI:4iWws5oP00,0*2F",1438900139
    "!AIVDM,1,1,,A,35DCJl100QoLlQ8BIKN<P:0D0>@<,0*19",1438478590
    "!AIVDM,1,1,,A,15MC0:000Ol9LalOLF:bk8bH086l,0*7B",1437222010
    "!AIVDM,1,1,,B,169EG;@P1::nTnlGm25U`wwJ28KB,0*6A",1435876966
    "!AIVDM,1,1,,A,14W9Ip0017GS>8dB<KvbA8N00<1=,0*22",1439466483
    "!AIVDM,1,1,,B,15N4r6P01FD2R>6O?n;F54WR0D04,0*33",1435748808
    "!AIVDM,1,1,,A,15RSMr001p9ho>B4CSBM3:Hp0h@P,0*4D",1441389209
    "!AIVDM,1,1,,B,1HL20h001qo2Uu6JQii;0HkN0>`<,0*5E",1439727293
Some messages may have been garbled or corrupted during transmission, resulting in incorrect checksums or message lengths. A link in the resources section is provided to calculate the checksum of each message.

The data is split into two files: one for training available here and another for testing available here. The provided training data file contains the raw AIS position report messages along with the decoded information. The ground truth for each of these rows is in the final column (FISHING_STATUS). The training data file has the following columns:

TIMESTAMP - Time in Unix epoch format
TIME - Time in human readable format
MESSAGE_ID - Message type
MMSI - Vessel identification number (not necessarily unique to a s
LAT - Current latitude
LONG - Current longitude
POS_ACCURACY - Indicates position accuracy
NAV_STATUS - Indicates navigational status
SOG - Speed over ground
COG - Course over ground
TRUE_HEADING - Heading
RAW_MESSAGE - Full raw AIS position report message
FISHING_STATUS - Fishing status (Fishing, Not Fishing, or Unknown)
The provided testing data file will only contain the columns TIMESTAMP and RAW_MESSAGE. Your program should read in data from the provided data files, and output a csv file containing the confidence predictions of the fishing status for each vessel at each point in time, one for every row in the testing data set. For example, a fishing confidence of 0.0 indicates that the vessel is definitely not fishing at this point in time while a fishing confidence of 1.0 indicates that the vessel is definitely fishing at this point in time. Your output file should contain only one confidence prediction per line in the same order as the provided testing data file. Line N of your output file corresponds to the Nth message (line) in the provided testing data file. Each line should contain only one human readable number between 0 and 1 indicating the fishing confidence for the corresponding message.