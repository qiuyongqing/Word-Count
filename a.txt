#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

using namespace std;

FILE *fp;

int chars = 0, space=0;

int charCount(char a)
{
    chars++;
    if(a==' ' || a == ',')
    {
        space++;
    }
}

void wordCount()
{
    char c;
    while(!feof(fp))
    {
        fscanf(fp,"%c",&c);

        charCount(c);
    }
}

void readWord(char* name)
{
    if((fp=fopen(name,"r+"))==NULL){
        printf("Open the file failure...\n");
        exit(0);
    }
    fp=fopen(name,"r");
    wordCount();

    fclose(fp);
}

void showWord(char para)
{
    if (para == 'w') {
        printf("总的单词数：%d\n",space + 1);
    } else if (para == 'c') {
        printf("总的字符数：%d\n",chars);
    } else {
        printf("参数错误！");
    }

}


int main(int argc, char* argv[])
{
    char para;
    para = getopt(argc,argv,"w:c:");
    char* name = optarg;
    readWord(name);
    showWord(para);
}