```
import (
    "sort"
)
var results [][]int
var note int
func permuteUnique(nums []int) [][]int {
    results = nil
    note = -1
    sort.Ints(nums)
    var res []int
    var positions = make(map[int]int, len(nums))
    traversal(res, nums, positions)
    return results
}

func traversal(res, nums []int, positions map[int]int){
    if len(res)==len(nums){
        // fmt.Println(res)
        results = append(results, res)
        return
    }
    for i := 0; i<len(nums); i++{
        if _, ok := positions[i]; ok||(note>=0&&nums[note]==nums[i]){
            continue
        }
        note = -1
        cp := make([]int, len(res))
        copy(cp, res)
        cp = append(cp, nums[i])
        positions[i] = i
        traversal(cp, nums, positions)
        delete(positions, i)
        note = i
    } 
}
```
