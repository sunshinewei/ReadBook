#### ViewModel

新建Viewmodel类，继承ViewModel，在此方法里进行更新Ui:
<pre><code>
 // Create a LiveData with a String
    private MutableLiveData<String> mCurrentName;
    // Create a LiveData with a String list
    private MutableLiveData<List<String>> mNameListData;

    public MutableLiveData<String> getCurrentName() {
        if (mCurrentName == null) {
            mCurrentName = new MutableLiveData<>();

            mCurrentName.postValue("aaaaaaaaaaaaaaa");
        }
        return mCurrentName;
    }

    public MutableLiveData<List<String>> getNameList() {
        if (mNameListData == null) {
            mNameListData = new MutableLiveData<>();
        }
        return mNameListData;
    }
</code></pre>