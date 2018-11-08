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

调用时：
 teastViewModel=ViewModelProviders.of(this).get(TeastViewModel.class);
 teastViewModel.getMutableLiveData().observe(this, new Observer<ProDetailBean>() {
      @Override
      public void onChanged(@Nullable ProDetailBean proDetailBean) {
           btn_save.setText(proDetailBean.getName());
      }
 });
