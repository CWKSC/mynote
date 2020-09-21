# C++

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int size = nums.size();
        for(int i = 0; i < size; i++) 
            for(int j = i + 1; j < size; j++) 
                if(nums[i] + nums[j] == target)
                    return {i, j};
        throw "Can't find";
    }
};
```





```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int size = nums.size();
        for(int i = 0;; ++i){
            int another = target - nums[i];
            for(int j = i + 1; j < size; ++j)
                if(another == nums[j])
                    return {i, j};
        }
        throw "Can't find";
    }
};
```





```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hashTable;
        for(int i = 0; i < nums.size(); i++) {
            hashTable[nums[i]] = i;
        }
        for(int i = 0; i < nums.size(); i++){
            int another = target - nums[i];
            if(hashTable.find(another) != hashTable.end()){
                if(hashTable[another] == i) continue;
                if(hashTable[another] < i){
                    return {hashTable[another], i};
                }else{
                    return {i, hashTable[another]};
                }
            }
        }
        throw "";
    }
};
```








```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int nums0 = nums[0];
        int nums1 = nums[1];
        unordered_map<int, int> map ={{nums0, 0}, {nums1, 1}};
        if(nums0 + nums1 == target) return {0, 1};
        for (int i = 2;; ++i) {
            int num = nums[i];
            int another = target - num;
            if(map.count(another))
                return {map[another], i};
            map[num] = i;
        }
        throw "";
    }
};
```







```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map = {{nums[0], 0}};
        int size = nums.size();
        for (int i = 1; i < size; i++) {
            int num = nums[i];
            int another = target - num;
            if(map.find(another) != map.end())
                return {map[another], i};
            map[num] = i;
        }
        throw "";
    }
};
```








```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map = {{nums[0], 0}, {nums[1], 1}};
        if(nums[0] + nums[1] == target) return {0, 1};
        int size = nums.size();
        for (int i = 2; i < size; i++) {
            int num = nums[i];
            auto iter = map.find(target - num);
            if(iter != map.end())
                return {iter->second, i};
            map[num] = i;
        }
        throw "";
    }
};
```







```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        auto begin = nums.begin();
        auto end = nums.end();
        int max = *max_element(begin, end);
        int min = *min_element(begin, end);
        int tryMax = target - min;
        int tryMin = target - max;
        if(tryMax > max) max = tryMax;
        if(tryMin < min) min = tryMin;
        //cout << "max: " << max << endl;
        //cout << "min: " << min << endl;
        //cout << "absMin: " << absMin << endl;
        int spaceSize = max - min + 1;
        if(spaceSize > 200){
            int nums0 = nums[0];
            int nums1 = nums[1];
            unordered_map<int, int> map ={{nums0, 0}, {nums1, 1}};
            if(nums0 + nums1 == target) return {0, 1};
            for (int i = 2;; ++i) {
                int num = nums[i];
                int another = target - num;
                if(map.count(another))
                    return {map[another], i};
                map[num] = i;
            }
            throw "";
        }
        
        vector<int> result(spaceSize);
        for(int i = 0; i < nums.size(); ++i){
            //cout << "index: " << nums[i] - min << endl;
            result[nums[i] - min]++;
        }
        //for(auto const& i : result) cout << i << " ";
        //cout << endl;
        for(int i = 0;; ++i){
            int another = target - nums[i];
            //cout << "another: " << another << endl;
            if(result[another - min]){
                int index = distance(begin, find(begin, end, another));
                //cout << index << ", " << i << endl;
                if(index == i) continue;
                return {index, i};
            }
        }
        //cout << "fail" ;
        throw "";
    }
};
```













