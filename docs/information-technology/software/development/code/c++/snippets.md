https://gist.github.com/skywarth/6b7db32e676224406570b215cfc738b3

### Sending multidimensional array to function as parameter
```cpp
#include <iostream>

using namespace std;

template <size_t rows, size_t cols, size_t k>
void three_dimension_parameter(int param1, int param2,int param3,int param4,int param5, int (&array)[rows][cols][k])
{
    cout<<array[param1][param2][param3]<<endl;
    
}

int main()
{
    cout<<"whaddup peeps"<<endl;
    
    int a[2][3][4];
    a[1][0][2]=420;
    int z,x,c,v,b;
    z=1;
    x=0;
    c=2;
    v=88;
    b=99;

    
    three_dimension_parameter(z,x,c,v,b,a);

    return 0;
}
```
