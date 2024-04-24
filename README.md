HIGH-DOSE MODELLING
https://github.com/yfzzzzz/Real_time-High-dose.git

Overview
The code enables loading desired rows of secondary electron data from unzipped archives. It retrieves secondary electron signals and separates them. Providing further analysis including curve fitting, exponential coefficients estimating, separating the area of each pulse, plotting, and making histograms. It may take about 1200 seconds to run without any plotting.

Installation
To download and install MATLAB, Simulink, and other MathWorks products:

1\ Sign in to your MathWorks Account or create a new one.

2\ Download your products from MathWorks Downloads.

3\ Follow the prompts to install the products for which you are licensed.

If you do not have a license for MathWorks products through an organization, such as a university or company, you can buy products or request a trial from the MathWorks Store.

How it works
The code is divided into six main parts: 1) UNZIP_FILES 2) Retrieval 3) Deterministic 4) Histograms 5) Model Verification: Theory and Experiment 6) Pulse shape tracking

Running an example
The first part is highly dependent on the name of the files.

files = zipdir(zipFilePath);
The code above will return a ‘struct’ which contains seven fields including: name, folder, data, uncompressedsize, isdir, canbeextracted, and datenum. It is necessary to run this line to check the desired information (keyword) for the next step retrieve. Such as the code below, which used the ‘folder’ and ‘name’.

if contains(files(i).folder, ' 200ns') && contains(files(i).folder, '25kV_Bi+/Mo') && contains(files(i).name, '#')
    i = i+1;    
end
Here it needs to take care of the keywords that are used to search during the ‘for’ loop. If the keywords have the same letter in the front, like ‘Si’ and ‘SiO’. It is necessary to put the ‘if’ loop of ‘SiO’ in front of ‘Si’, otherwise ‘SiO’ will be counted as ‘Si’. It cannot do a refined search.

There are other parts that require to adjust the value manually. First is the ‘Wind_dura’ that depends on the total duration of the detection window in the second. The second is the ‘findpeaks’ argument.

findpeaks(value_V_SE,indice_V_SE,"MinPeakProminence",20,"MinPeakDistance",100);
There is a part for tunning ‘MinPeakProminence’ and ‘MinPeakDistance’ by observing the pulse plot. The lower the noise, the easier the tunning.

The second part of ‘Retrieval’ is simply fitting and running automatically. As long as the right format (double) is assigned to ‘rowData’ (y-axis) and ‘tt’ (x-axis), it should be fine. All the parts after that just the additional functions which is replaceable.

Bugs & Feature Requests
Please report bugs and request features using the Issue Tracker.
