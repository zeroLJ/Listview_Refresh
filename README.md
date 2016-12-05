# Listview_Refresh
 更美观的下拉 刷新Listview
使用方法：

    1.把ptr-lib整个module导入到自己的项目中。（修改build.gradle文件 版本设置为与自己项目一样） 
    2.右键自己的module->open module setting->Dependencies把ptr-lib目录添加进去

    3.在layout的xml文件中使用
      <in.srain.cube.views.ptr.PtrClassicFrameLayout
        android:id="@+id/rotate_header_list_view"
        xmlns:cube_ptr="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        cube_ptr:ptr_duration_to_close="200"
        cube_ptr:ptr_duration_to_close_header="1000"
        cube_ptr:ptr_keep_header_when_refresh="true"
        cube_ptr:ptr_pull_to_fresh="false"
        cube_ptr:ptr_ratio_of_header_height_to_refresh="1.2"
        cube_ptr:ptr_resistance="1.7">
        <ListView
            android:id="@+id/msg_list_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:divider="@null"
            android:fadingEdge="none"
            android:listSelector="@android:color/transparent"
            android:paddingLeft="12dp"
            android:paddingRight="12dp"
            android:scrollbarStyle="outsideOverlay"
            android:choiceMode="singleChoice" />
    </in.srain.cube.views.ptr.PtrClassicFrameLayout>
    
    
    4.activity中：
     private PtrClassicFrameLayout mPtrFrame;
     
     
      msgListView= (ListView) findViewById(R.id.msg_list_view);
        mPtrFrame = (PtrClassicFrameLayout) findViewById(R.id.rotate_header_list_view);
        mPtrFrame.setLastUpdateTimeRelateObject(this);
        mPtrFrame.setPtrHandler(new PtrHandler() {
            @Override
            public void onRefreshBegin(PtrFrameLayout frame) {
                mPtrFrame.postDelayed(new Runnable() {
                    @Override
                    public void run() {
                        //在这写刷新要完成的代码

                        mPtrFrame.refreshComplete();//停止刷新效果
                    }
                }, 0);
            }
            @Override
            public boolean checkCanDoRefresh(PtrFrameLayout frame, View content, View header) {
                return PtrDefaultHandler.checkContentCanBePulledDown(frame, content, header);
            }
        });
        // the following are default settings
        mPtrFrame.setResistance(1.7f);
        mPtrFrame.setRatioOfHeaderHeightToRefresh(1.2f);
        mPtrFrame.setDurationToClose(200);
        mPtrFrame.setDurationToCloseHeader(1000);
        // default is false
        mPtrFrame.setPullToRefresh(false);
        // default is true
        mPtrFrame.setKeepHeaderWhenRefresh(true);
        /*mPtrFrame.postDelayed(new Runnable() {    //启动自动刷新一次
            @Override
            public void run() {
                mPtrFrame.autoRefresh();
            }
        }, 100);*/
