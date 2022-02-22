#include <stdio.h>

void fillArray(int arr[], int n);
void bubbleSort(int arr[], int n);
void selectionSort(int arr[], int n);
void swap(int *x, int *y);
void heapify(int arr[], int n, int i);
void heapSort(int arr[], int n);

int main()
{
    int n;
    printf("nhap n= ");
    scanf("%d", &n);
    if(n <= 3 || n >= 10){
        return 0;
    }
    int arr[n];
    for(int i = 0; i < n; i++){
        printf("Nhap so thu %d:", i+1);
        scanf("%d",&arr[i]);
    }
    printf("\nmang co cac phan tu:\n");
    fillArray(arr, n);
    printf("\nMang da sap xep bubbleSort:\n");
    bubbleSort(arr, n);
    fillArray(arr, n);
    printf("\nMang da sap xep selectionSort:\n");
    selectionSort(arr, n);
    fillArray(arr, n);
    printf("\nMang da sap xep heapify:\n");
    heapSort(arr, n);
    fillArray(arr, n);
    
}

void fillArray(int arr[], int n){
    for(int i = 0; i < n; i++){
        printf("%d ", arr[i]);
    }
}

void swap(int *x, int *y)
{
    *x = *x + *y;
    *y = *x - *y;
    *x = *x - *y;
}

void bubbleSort(int arr[], int n)
{
    int i, j;
    int haveSwap = 0;
    for (i = 0; i < n-1; i++){
        haveSwap = 0;
        for (j = 0; j < n-i-1; j++){
            if (arr[j] > arr[j+1]){
                swap(&arr[j], &arr[j+1]);
                haveSwap = 1; 
            }
        }
        if(haveSwap == 0){
            break;
        }
    }
}

void selectionSort(int arr[], int n)
{
   int i, j, idx, temp;
   for (i = 0; i < n-1; i++)
   {
       idx = i;
       for (j = i+1; j < n; j++)
       {
           if (arr[i] > arr[j])
           {
               idx = j;
               swap(&arr[i], &arr[idx]);
           }
       }
   }
}

void heapify(int arr[], int n, int i)
{  // mang arr, n - so phan tu i - dinh can vun dong
    int max =i;    // Luu vi tri dinh max ban dau
    int l = i*2 +1;   // Vi tri con trai
    int r = l+1;    // Vi tri con phai
    if(l<n && arr[l] > arr[max]){   // Neu ton tai con trai lon hon cha, gan max = L
        max = l;
    }
    
    if(r<n && arr[r] > arr[max]){   // Neu ton tai con phai lon hon arr[max], gan max = r
        max = r;
    }
    if(max != i){      // Neu max != i, tuc la cha khong phai lon nhat
        swap(&arr[i], &arr[max]);   // doi cho cho phan tu lon nhat lam cha
        heapify(arr ,n , max);    // Ðe quy vun cac node phia duoi
    }
    
}

void heapSort(int arr[], int n)
{
    
    // vun dong tu duoi len len de thanh heap
    for(int i = n/2 - 1; i>=0; i--)   // i chay tu n/2 - 1 ve 0 se co n/2 dinh
        heapify(arr,n, i);   // Vun tung dinh
    
    // Vong lap de thuc hien vun dong va lay phan tu
    for(int j = n-1 ; j>0; j--){   // chay het j == 1 se dung
                // moi lan j - 1, tuong duong voi k xet phan tu cuoi 
        swap(&arr[0], &arr[j] );  // doi cho phan tu lon nhat
             heapify(arr, j, 0);    // vun lai dong, 
    }
}
