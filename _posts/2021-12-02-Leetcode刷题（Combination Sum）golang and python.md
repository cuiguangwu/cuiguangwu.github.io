```
import (
    "sort"
)
var results [][]int
func combinationSum(candidates []int, target int) [][]int {
    results = nil
    sort.Ints(candidates)
    var result []int
    // fmt.Println(candidates)
    traversal(len(candidates)-1, target, result, candidates)
    
    return results
}

func traversal(start, tempNum int, result, candidates []int){
    if tempNum<candidates[0]|| tempNum==0{
        if tempNum==0{
            // fmt.Println(result)
            results = append(results, result)
        }
        return
    }
    for i:=start; i>=0; i--{
        if tempNum >= candidates[i]{
            result = append(result, candidates[i])
            cp := make([]int, len(result))
            copy(cp, result)
            traversal(i, tempNum - candidates[i], cp, candidates)
            result = result[:len(result)-1]
        }   
    }
}




func digui(start, tempNum int, result []int, candidates []int){
    if tempNum<candidates[0]||start<0{
        return
    }
    for j:=start; j>=0; j--{
        n := tempNum / candidates[j]
        tempNum = tempNum % candidates[j]
        for k:=0; j<n; k++{
            result = append(result, candidates[j])
        }
      
        if tempNum==0{
            cp := make([]int, len(result))
            results = append(results, cp)
            // result.Remove("xxx")
        }
        n--
        tempNum += candidates[j]
        
        digui(start-1, tempNum, result, candidates)  
    }
    return
}

PYTHON 版本
```
class Solution:
    res = []
    flag = False
    
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        self.res = []
        track = []
        
        candidates.sort(reverse=True)
        self.traversal(candidates, target, track, 0)
        return self.res
        
    def traversal(self, candidates, target, track, i):
        tmp = target 
        if track:
            for j in track:
                tmp -= candidates[j]
        while i < len(candidates):
            if candidates[i] > tmp:
                i += 1
            else:
                tmp = tmp - candidates[i]
                track.append(i)                
                if not tmp:
                    self.flag = True
                    break
        if not track and i == len(candidates):
             return
            
        tmpCandidate = [candidates[j] for j in track]
        if self.flag:
            self.res.append(tmpCandidate)
            self.flag = False
        
        i = track.pop()
   
        self.traversal(candidates, target, track,i+1)
       
