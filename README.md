# Cara Membuat gui matlab
# Langkah-langkahnya yaitu:

# 1. Membuka aplikasi software Matlab

![tampilan-matlab](https://user-images.githubusercontent.com/56244029/117444783-2195fc00-af64-11eb-898a-f3e136d402d4.jpg)

2. Membuka GUIDE Matlab dengan cara mengetik “guide” pada command window dan tekan enter, sehingga muncul tampilan seperti pada gambar di bawah ini

![tampilan-gui-matlab](https://user-images.githubusercontent.com/56244029/117444891-3d010700-af64-11eb-9829-3f532ea064f5.jpg)

atau klik menu New >> Graphical User Interface seperti yang ditunjukkan pada gambar berikut

![tampilan-graphical-user-interface-gui-matlab](https://user-images.githubusercontent.com/56244029/117444925-4db17d00-af64-11eb-9546-5a173eb6550a.jpg)

3. Klik “Ok” pada GUIDE Quick Start >> Create New GUI >> Blank GUI (default)

![tampilan-graphical-user-interface-gui-matlab-2](https://user-images.githubusercontent.com/56244029/117445003-63bf3d80-af64-11eb-8e7d-2ba80a152eb4.jpg)

sehingga akan muncul tampilan GUIDE Matlab seperti pada gambar berikut

![4](https://user-images.githubusercontent.com/56244029/117445053-720d5980-af64-11eb-86f5-793e0b774b4d.jpg)

4. Untuk menampilkan nama palet komponen, klik File >> Preferences

![tampilan-graphical-user-interface-gui-matlab](https://user-images.githubusercontent.com/56244029/117445095-805b7580-af64-11eb-8e98-7ceb2c34c74c.jpg)

kemudian beri tanda centang (√) pada menu Show names in component palette lalu klik “Ok”

![6](https://user-images.githubusercontent.com/56244029/117445149-92d5af00-af64-11eb-853b-b6a5352c406f.jpg)

sehingga akan muncul tampilan seperti pada gambar di bawah ini

![7](https://user-images.githubusercontent.com/56244029/117445191-9cf7ad80-af64-11eb-8b6f-feeedb31c9b0.jpg)

5. Buatlah rancangan GUI MATLAB yang terdiri dari 2 axes, 3 pushbutton, 1 slider, dan 1 edit text seperti tampak pada gambar di bawah ini

![tampilan-desain-gui-matlab](https://user-images.githubusercontent.com/56244029/117445239-a97c0600-af64-11eb-9d9f-2e96da3faad1.jpg)

6. Editlah property masing-masing komponen dengan cara meng-double klik setiap komponen lalu mengganti propertynya sesuai dengan tabel berikut

No	Nama Komponen	Property	Nilai
1	Pushbutton	String	Open Image
Tag	pushbutton1
2	Pushbutton	String	Grayscale
Tag	pushbutton2
3	Pushbutton	String	Save
Tag	pushbutton3
4	Slider	min	0
max	255
tag	slider1
5	Edit Text	String	<kosongkan>
6	Axes	XTick	<kosongkan>
YTick	<kosongkan>
ZTick	<kosongkan>
7	Axes	XTick	<kosongkan>
YTick	<kosongkan>
ZTick	<kosongkan>
sehingga tampilan GUI tampak pada gambar berikut:
  
  ![8](https://user-images.githubusercontent.com/56244029/117445303-bc8ed600-af64-11eb-8b25-0b58f373665c.jpg)
  
  
  6. Listing Program untuk pusbutton1 (tombol buka citra) adalah

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[name_file1,name_path1] = uigetfile( ...
    {'*.bmp;*.jpg;*.tif','Files of type (*.bmp,*.jpg,*.tif)';
    '*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Open Image');
 
if ~isequal(name_file1,0)
    handles.data1 = imread(fullfile(name_path1,name_file1));
    guidata(hObject,handles);
    axes(handles.axes1);
    imshow(handles.data1);
else
    return;
end
Listing Program untuk pusbutton2 (konversi citra RGB menjadi grayscale)

1
2
3
4
5
6
7
8
9
10
11
% --- Executes on button press in pushbutton2.
function pushbutton2_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
image1 = handles.data1;
gray = rgb2gray(image1);
axes(handles.axes2);
imshow(gray);
handles.data2 = gray;
guidata(hObject,handles);
Listing Program untuk slider1 (konversi citra grayscale menjadi biner)

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
% --- Executes on slider movement.
function slider1_Callback(hObject, eventdata, handles)
% hObject    handle to slider1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
 
% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
gray = handles.data2;
value = get(handles.slider1,'value');
thresh = imcomplement(im2bw(gray,value/255));
axes(handles.axes2);
imshow(thresh);
handles.data3 = thresh;
guidata(hObject,handles);
set(handles.edit1,'String',value)
Listing Program untuk pushbutton3 (menyimpan citra biner hasil konversi)

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
% --- Executes on button press in pushbutton3.
function pushbutton3_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
thresh = handles.data3;
[name_file_save,path_save] = uiputfile( ...
    {'*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Save Image');
if ~isequal(name_file_save,0)
    imwrite(thresh,fullfile(path_save,name_file_save));
else
    return
end
Sedangkan listing program lengkapnya adalah sbb:

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
102
103
104
105
106
107
108
109
110
111
112
113
114
115
116
117
118
119
120
121
122
123
124
125
126
127
128
129
130
131
132
133
134
135
136
137
138
139
140
141
142
143
144
145
146
147
148
149
150
151
152
153
154
155
156
157
158
159
160
161
162
163
164
165
166
167
168
169
170
171
172
173
174
175
176
177
function varargout = Konversi_Biner(varargin)
% KONVERSI_BINER M-file for Konversi_Biner.fig
%      KONVERSI_BINER, by itself, creates a new KONVERSI_BINER or raises the existing
%      singleton*.
%
%      H = KONVERSI_BINER returns the handle to a new KONVERSI_BINER or the handle to
%      the existing singleton*.
%
%      KONVERSI_BINER('CALLBACK',hObject,eventData,handles,...) calls the local
%      function named CALLBACK in KONVERSI_BINER.M with the given input arguments.
%
%      KONVERSI_BINER('Property','Value',...) creates a new KONVERSI_BINER or raises the
%      existing singleton*.  Starting from the left, property value pairs are
%      applied to the GUI before Konversi_Biner_OpeningFcn gets called.  An
%      unrecognized property name or invalid value makes property application
%      stop.  All inputs are passed to Konversi_Biner_OpeningFcn via varargin.
%
%      *See GUI Options on GUIDE's Tools menu.  Choose "GUI allows only one
%      instance to run (singleton)".
%
% See also: GUIDE, GUIDATA, GUIHANDLES
 
% Edit the above text to modify the response to help Konversi_Biner
 
% Last Modified by GUIDE v2.5 24-Jul-2015 02:44:32
 
% Begin initialization code - DO NOT EDIT
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
    'gui_Singleton',  gui_Singleton, ...
    'gui_OpeningFcn', @Konversi_Biner_OpeningFcn, ...
    'gui_OutputFcn',  @Konversi_Biner_OutputFcn, ...
    'gui_LayoutFcn',  [] , ...
    'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end
 
if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End initialization code - DO NOT EDIT
 
 
% --- Executes just before Konversi_Biner is made visible.
function Konversi_Biner_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% varargin   command line arguments to Konversi_Biner (see VARARGIN)
 
% Choose default command line output for Konversi_Biner
handles.output = hObject;
movegui(hObject,'center')
 
% Update handles structure
guidata(hObject,handles);
 
% UIWAIT makes Konversi_Biner wait for user response (see UIRESUME)
% uiwait(handles.figure1);
 
 
% --- Outputs from this function are returned to the command line.
function varargout = Konversi_Biner_OutputFcn(hObject, eventdata, handles)
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
 
% Get default command line output from handles structure
varargout{1} = handles.output;
 
 
% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
[name_file1,name_path1] = uigetfile( ...
    {'*.bmp;*.jpg;*.tif','Files of type (*.bmp,*.jpg,*.tif)';
    '*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Open Image');
 
if ~isequal(name_file1,0)
    handles.data1 = imread(fullfile(name_path1,name_file1));
    guidata(hObject,handles);
    axes(handles.axes1);
    imshow(handles.data1);
else
    return;
end
 
% --- Executes on button press in pushbutton2.
function pushbutton2_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
image1 = handles.data1;
gray = rgb2gray(image1);
axes(handles.axes2);
imshow(gray);
handles.data2 = gray;
guidata(hObject,handles);
 
% --- Executes on slider movement.
function slider1_Callback(hObject, eventdata, handles)
% hObject    handle to slider1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
 
% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
gray = handles.data2;
value = get(handles.slider1,'value');
thresh = imcomplement(im2bw(gray,value/255));
axes(handles.axes2);
imshow(thresh);
handles.data3 = thresh;
guidata(hObject,handles);
set(handles.edit1,'String',value)
 
% --- Executes on button press in pushbutton3.
function pushbutton3_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
thresh = handles.data3;
[name_file_save,path_save] = uiputfile( ...
    {'*.bmp','File Bitmap (*.bmp)';...
    '*.jpg','File jpeg (*.jpg)';
    '*.tif','File Tif (*.tif)';
    '*.*','All Files (*.*)'},...
    'Save Image');
if ~isequal(name_file_save,0)
    imwrite(thresh,fullfile(path_save,name_file_save));
else
    return
end
 
% --- Executes during object creation, after setting all properties.
function slider1_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called
 
% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end
 
 
function edit1_Callback(hObject, eventdata, handles)
% hObject    handle to edit1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
 
% Hints: get(hObject,'String') returns contents of edit1 as text
%        str2double(get(hObject,'String')) returns contents of edit1 as a double
 
 
% --- Executes during object creation, after setting all properties.
function edit1_CreateFcn(hObject, eventdata, handles)
% hObject    handle to edit1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called
 
% Hint: edit controls usually have a white background on Windows.
%       See ISPC and COMPUTER.
if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end

7. Ketika di Run maka tampilan GUI akan tampak seperti pada gambar di bawah ini

![9](https://user-images.githubusercontent.com/56244029/117445397-d3352d00-af64-11eb-90bf-a345f7e512c8.jpg)


8. Klik Open Image, pilih gambar yang ingin diproses

![tampilan-buka-citra-gui-matlab1](https://user-images.githubusercontent.com/56244029/117445448-e2b47600-af64-11eb-9c2d-11eda6dcd979.jpg)

9. Klik Grayscale

![konversi-citra-rgb-menjadi-grayscale-gui-matlab](https://user-images.githubusercontent.com/56244029/117445485-ed6f0b00-af64-11eb-9a31-4120d694a243.jpg)

10. Geser nilai Slider

![konversi-citra-rgb-menjadi-grayscale-gui-matlab](https://user-images.githubusercontent.com/56244029/117445527-fbbd2700-af64-11eb-9bf5-4a73cc03a728.jpg)

11. Citra biner yang terbentuk dapat disimpan dengan cara meng-klik tombol Save Image
