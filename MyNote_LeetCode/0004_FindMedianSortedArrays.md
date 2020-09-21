# C#

```c#
public class Solution {
    public static T[] SortTwoSortedArray<T>(T[] A, T[] B) where T : IComparable
    {
        int aLength = A.Length;
        int bLength = B.Length;
        if (aLength == 0) { return (T[])B.Clone(); }
        if (bLength == 0) { return (T[])A.Clone(); }
        T[] result = new T[aLength + bLength];
        int i = 0, j = 0, resultIndex = 0;
        while (true)
        {
            result[resultIndex++] = A[i].CompareTo(B[j]) < 0 ? A[i++] : B[j++];
            if (i == aLength)
            {
                Array.Copy(B, j, result, resultIndex, bLength - j);
                break;
            }
            else if(j == bLength)
            {
                Array.Copy(A, i, result, resultIndex, aLength - i);
                break;
            }
        }
        return result;
    }
    public double FindMedianSortedArrays(int[] nums1, int[] nums2) {
        int[] result = SortTwoSortedArray(nums1, nums2);
        int length = result.Length;
        int half = length >> 1;
        return (length & 1) == 0 ? (result[half-1] + result[half]) / 2.0 : result[half];
    }
}
```

