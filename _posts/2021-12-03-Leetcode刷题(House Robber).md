```
import (
    "fmt"
)
var maxNum int
var table []int
func rob(nums []int) int {
    maxNum = 0
    table = nil
    table = make([]int, len(nums))
    for i:=0; i<len(nums); i++{
        table[i] = -1
    }
    
    if len(nums)==1{
        return nums[0]
    }
    
    for i:=len(nums)-2; i>=0; i-- {
        maxNum = 0
        digui(i, 0, nums)
    }
    fmt.Println(maxNum, table)
    return table[0]
}

func digui(start, cnt int, nums []int){
    if start+1>=len(nums)-1{
        maxNum = max(cnt+nums[start], maxNum)
        if start+1==len(nums)-1{
            table[start+1] = cnt+nums[start+1]
            maxNum = max(table[start+1] , maxNum)
        }
        table[start] = maxNum
        return        
    }
    
    if start+2<len(table) && table[start+2]>=0{
        table[start] = nums[start] + table[start+2]
        table[start] = max(table[start] , table[start+1])
        return
    }
    digui(start+2, cnt+nums[start], nums)
    digui(start+1, cnt, nums)
   
    
    table[start] = maxNum
    return
}

func max(num1, num2 int) int {
    if num1>num2{
        return num1
    }
    return num2
}
