# MINOR-PROJECT
%Fingerprint Minutiae Extraction
%Programming language used is MATLAB'.
%Here is the code below:-
%Program for Fingerprint Minutiae Extraction
%Program Description
%This program extracts the ridges and bifurcation from a fingerprint image
%Read Input Image
img=imread('C:\Users\hp\Dessktop\input_1.tif');
figure(1);
imshow(img);
title('Input image');
%Binarization
binImg=imbinarize(img);
binImg = binImg120:400,20:250); %Considering a portion of image
figure(2);
imshow(binImg);
title('Binary image');
%Thinning
thinImg=~bwmorph(binImg,'thin',Inf);
figure(3);
imshow(thinImg);
title('Thinned Image');
%Minutiae extraction
s=size(thinImg);
N=3; %window size
n=(N-1)/2;
r=s(1)+2*n;
c=s(2)+2*n;
double temp(r,c);
temp=zeros(r,c);
bifurcation=zeros(r,c);
ridge=zeros(r,c);
temp((n+1):(end-n),(n+1):(end-n))=thin_image(:,:); %n pixel thick boundary
outImg=zeros(r,c,3);
%For Display
outImg(:,:,1) = temp .* 255;
outImg(:,:,2) = temp .* 255;
outImg(:,:,3) = temp .* 255;
for x=(n+1+5):(s(1)+n-5)
 for y=(n+1+5):(s(2)+n-5)
 a=1;
 for k=x-n:x+n
 b=1;
 for l=y-n:y+n
 mat(a,b)=temp(k,l);
 b=b+1;
 end
 a=a+1;
 end;
 if(mat(2,2)==0)
 ridge(x,y)=sum(sum(~mat));
 bifurcation(x,y)=sum(sum(~mat));
 end
 end
end
% Finding ridge endings
[rx ry]=find(ridge==2);
len=length(rx);
%For Display
for i=1:len
 outImg((rx(i)-3):(rx(i)+3),(ry(i)-3),2:3)=0;
 outImg((rx(i)-3):(rx(i)+3),(ry(i)+3),2:3)=0;
 outImg((rx(i)-3),(ry(i)-3):(ry(i)+3),2:3)=0;
 outImg((rx(i)+3),(ry(i)-3):(ry(i)+3),2:3)=0;

 outImg((rx(i)-3):(rx(i)+3),(ry(i)-3),1)=255;
 outImg((rx(i)-3):(rx(i)+3),(ry(i)+3),1)=255;
 outImg((rx(i)-3),(ry(i)-3):(ry(i)+3),1)=255;
 outImg((rx(i)+3),(ry(i)-3):(ry(i)+3),1)=255;
end
%Finding bifurcation
[bx by]=find(bifurcation==4);
len=length(bx);
%For Display
for i=1:len
 outImg((bx(i)-3):(bx(i)+3),(by(i)-3),1:2)=0;
 outImg((bx(i)-3):(bx(i)+3),(by(i)+3),1:2)=0;
 outImg((bx(i)-3),(by(i)-3):(by(i)+3),1:2)=0;
 outImg((bx(i)+3),(by(i)-3):(by(i)+3),1:2)=0;

 outImg((bx(i)-3):(bx(i)+3),(by(i)-3),3)=255;
 outImg((bx(i)-3):(bx(i)+3),(by(i)+3),3)=255;
 outImg((bx(i)-3),(by(i)-3):(by(i)+3),3)=255;
 outImg((bx(i)+3),(by(i)-3):(by(i)+3),3)=255;
end
  
 
