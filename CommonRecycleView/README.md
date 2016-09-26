#### ͨ�õ�RecycleViewAdapter��RecycleViewHolder

##### ��ǰ������ʹ��ListView��ʱ��Ҳ������ʹ�õ���װ��ListView����߿���Ч�ʣ�������RecycleViewҲ��һ���ģ�������߿���Ч�ʣ�

##### ������˵��˵һ�����Ǿ����ʹ�÷�ʽ����ǰ����ʹ��RecycleView��ʱ�����Ƕ���ʹ�ø��ݹٷ��ṩ��ʵ����д������ÿһ�ζ�Ҫ���´�����������ViewHolder�����鷳�����дһ��ͨ�õ�Adapter��ViewHoler��ô�ͷ���ĺܶࣻ
-----------------------------------


##### �������ǿ�һ�°�����Ϊ�ձ��RecycleView��ʹ�õĴ��롣

###### ��Ҫ��������������

-  ���Ȼ�ȡRecycleView��ʵ����������չʾ��ʽ�Լ���������
-  ��δ����������̳�RecycleViewAdapter
-  ֮�󴴽�ViewHolder�̳�RecycleView.ViewHolder
------------

###### һ,��ȡRecycleView��ʵ�������ø�������

```xml
 mRecyclerView = (RecyclerView) findViewById(R.id.recycleview);
        //�����б�չʾ����
        LinearLayoutManager layoutManager = new LinearLayoutManager(this);
        //�����ķ���
        layoutManager.setOrientation(OrientationHelper.VERTICAL);
        //����Item���ӡ��Ƴ�����
        mRecyclerView.setItemAnimator(new DefaultItemAnimator());

        mRecyclerView.setLayoutManager(layoutManager);
        
        mRecyclerView.setAdapter(myAdapter);

```

###### ��,����MyHolderView

```xml
public class MyHolderView extends RecyclerView.ViewHolder{

        private View itemViews;
        private TextView title;
        private ImageView imageView;
        public MyHolderView(View itemView) {
            super(itemView);
            itemViews = itemView.findViewById(R.id.cardviews);
            title = (TextView) itemView.findViewById(R.id.titles);
            imageView = (ImageView) itemView.findViewById(R.id.imageview);
        }
    }
```

###### ��������Adapter

```xml

public class RecycleAdapter extends RecyclerView.Adapter<MyHolderView> implements View.OnClickListener{

        //���õ�item�ĵ���¼�������
        private RecycleItemClickListener mRecycleItemClickListener;

        public void setRecycleItemClickListener(RecycleItemClickListener mRecycleItemClickListener) {

            this.mRecycleItemClickListener = mRecycleItemClickListener;
        }
        //�󶨲��֣�Ҳ����ViewHolder
        @Override
        public MyHolderView onCreateViewHolder(ViewGroup parent, int viewType) {

            View view = mLayoutInflater.inflate(R.layout.item_layout, parent, false);
            MyHolderView myHolderView = new MyHolderView(view);
            myHolderView.itemViews.setOnClickListener(this);
            return myHolderView;
        }

        //���ݰ󶨵Ĳ��֣���ȡ�ؼ�����������
        @Override
        public void onBindViewHolder(MyHolderView holder, int position) {
            holder.imageView.setVisibility(View.VISIBLE);
            app.imageLoader.displayImage(mImagePath.get(position), holder.imageView);
            holder.title.setText(mImagePath.get(position));
//            holder.itemView.setTag(mImagePath.get(position));
            holder.itemViews.setTag(position);
        }

        //���е�����Դ������
        @Override
        public int getItemCount() {
            return mImagePath.size();
        }

        @Override
        public void onClick(View v) {

            try {
                int position = (int) v.getTag();
                Log.e(TAG, ""+position);
                if(mRecycleItemClickListener != null)
                    mRecycleItemClickListener.onRecycleItemClickListener(v,position);
            }catch (Exception e){
                Log.e(TAG ,"click:"+e.getMessage());
            }

        }
    }

```

###### ֮���ǲ����ļ�
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:layout_marginLeft="4dp"
    android:layout_marginRight="4dp"
    tools:context="com.base.translucents.MainActivity">


    <android.support.v7.widget.RecyclerView
        android:visibility="gone"
        android:id="@+id/recycleview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>


    <android.support.v4.widget.ContentLoadingProgressBar
        android:visibility="visible"
        android:id="@+id/progress"
        style="?android:attr/progressBarStyleLarge"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:indeterminate="false" />

</LinearLayout>
```
###### �����RecycleView�ϵ�Item����

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:background="@drawable/ripple_bg"
    android:id="@+id/content"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal">

    <de.hdodenhof.circleimageview.CircleImageView
        android:layout_margin="8dip"
        android:id="@+id/head"
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:layout_gravity="center"
        android:src="@drawable/small"
        app:border_color="@android:color/white"
        app:border_width="2dp" />

    <TextView
        android:textSize="16sp"
        android:layout_margin="8dip"
        android:id="@+id/titles"
        android:layout_width="0dip"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:gravity="center"
        android:text="dizhi" />
</LinearLayout>


```

------------------------

###### ͨ�����ǿ�ʼдRecycleView��ʱ��������д�ģ����ÿһ�����б��ʱ������дһ�������Ǻ����鷳�𣬾��㲻�鷳�Լ�������дҲ���µģ�����Ҫ��....

##### ��������Ҫд�������ʱ��Ҫ���ȿ�������ʵ���ԣ����ԣ��Ͱ�ȫ�ԣ��Լ���׳�Ժ����ܵ������ȵȣ���Ҫ���ǵ�������дһ��������ֻ����ʵ���Ժ������ԣ�����������Ҳ�ǲ��еġ��������Ǵ��⼸�����濼�ǡ�
- 1��������AdapterҪ������Դ���뵽������Adapter�У����������ڶ�����Դ�İѿغͲ�������Ҫ��Context������Դ���Լ�Item���ִ����ȥ�� 2�����⣬��onBindViewHolder�����н��ؼ��Ӵ��������ViewHolder���ó������������ݣ����������ֻ����Adapter�е�onBindViewHolder����ʵ�֣�
- 3������ViewHolder��ʱ��ÿ�ζ�Ҫ�������������еĿؼ�����ʼ��һ�飬Ҳ�����鷳��
- 4�������ݵ�Listʵ����ʾ��ͬ������ʵ��Ҳ�ǲ�һ���ģ���ʵ�岻һ����ʱ�����Ǿ�Ҫ���´���һ��������������Ȼ���Ǻܲ���ȡ�ģ�


##### ����������ڴ���Adapter��ʱ����������׳���Activity�л���Fragmentʹ���ǲ��Ƿ���Ķ��ˣ����ÿ���Adapter�ͣ�ViewHolder�ڲ�����ôʵ�ֵģ�ֱ�ӷ�װ�ã�ֻ����onBindViewHolder�ؼ����ݵ����룬����ʾ��������ô��������С�˺ܶࣻ

##### ���������ǾͰ��������ᵽ�ģ��鷳��һ�����

*************************

##### һ����������ô������һ������������Ҫ�Ĳ������ݴ��뵽�������У�

##### �����ͨ���������Ĺ��췽������Context������Դ���Լ�item��id���룻

##### ���ԣ��������д�ɣ�
```xml
/**
     * �����߼����˽���������ʹ��
     * @param holder CommonRecycleViewHolder
     * @param position ��ǰ����item��λ��
     */
    public abstract void onCommonBindViewHolder(CommonRecycleViewHolder holder, int position);
    private Context context;
    private List<T> datas;
    private LayoutInflater mLayoutInflater;
    private int layoutId;
    public  CommonRecycleAdapter(Context context, List<T> datas, int layoutId) {

        //����������������Ҫ�Ĳ���������ô��
        this.context = context;
        this.datas = datas;
        this.layoutId = layoutId;
        this.mLayoutInflater = LayoutInflater.from(context);
    }
    
    //���������л�ȡViewholder�����ҷ���
     @Override
    public CommonRecycleViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return new CommonRecycleViewHolder(mLayoutInflater.inflate(layoutId, parent, false));
    }
    
```





##### ������������ô�����ܽ���ȡ�ؼ��ķ��������׸�������onBindViewHolder���õ��������ⲿʹ�ã�

##### ��������Խ�Adapter���������ɳ����abstract��֮��������һ������ķ�������дonBindViewHolder��������Ϳ��Կ��Ʋ�����item�����ؼ��ļ����¼��ˣ�

##### ���ԣ��������д�ɣ�
```xml
 /**
     * �����߼����˽���������ʹ��
     * @param holder CommonRecycleViewHolder
     * @param position ��ǰ����item��λ��
     */
    public abstract void onCommonBindViewHolder(CommonRecycleViewHolder holder, int position);
    
     @Override
    public void onBindViewHolder(CommonRecycleViewHolder holder, int position) {

        /**
         * ��Adapter��Ϊ�����࣬�����ṩ����ķ�����
         * ʹonBindViewHolder������д�������չʹ��
         */
        onCommonBindViewHolder(holder, position);
    }
    
    
    //��󵱵����ߴ���Adapter��ʱ�򣬾Ϳ������ⲿʹ��onBindViewHolder�������ĳ��󷽷���onCommonBindViewHolder��
    
     /**
         * �󶨵�����ֵ�׵�����ʹ��
         */
        adapter = new CommonRecycleAdapter(this, datas, R.layout.item_layout) {
            @Override
            public void onCommonBindViewHolder(CommonRecycleViewHolder holder, final int position) {

                final AppInfo info = datas.get(position);
                holder.setImageDrawable(R.id.icons, info.appIcon);
                holder.setText(R.id.titles, info.appName);

                /**
                 * ���ü����¼�
                 */
//                holder.setViewListener(R.id.icons, new CommonRecycleViewHolder.SetOnViewClickListener() {
//                    @Override
//                    public void onViewListener(View view) {
//
//                        Log.e("MainActivity.class", ""+info.appName);
//                    }
//                });
//
//                holder.setViewListener(R.id.titles, new CommonRecycleViewHolder.SetOnViewClickListener() {
//                    @Override
//                    public void onViewListener(View view) {
//
//                        Log.e("MainActivity.class", ""+position);
//                    }
//                });

                holder.setViewListener(R.id.items, new CommonRecycleViewHolder.SetOnViewClickListener() {
                    @Override
                    public void onViewListener(View view) {

                        Log.e("MainActivity.class", "��ǰ"+info.appPackName);
                    }
                });
            }
        };

```

##### ���⻹������Adapter�д���������������Դ�ķ����������������Դ�����룬�滻���ȵȣ�����
```xml
/**
     * ��������
     * @param newDatas
     */
    public void addDatas(List<T> newDatas) {

        if (datas != null && newDatas != null){
            datas.addAll(newDatas);
        }
    }

    /**
     * ��������
     * @param datas
     */
    public void resetDatas(List<T> datas) {

        try {

            if (this.datas != null){
                this.datas.clear();

                if (datas != null) {
                    this.datas.addAll(datas);
                }
            }

        }catch (Exception e) {
            e.printStackTrace();
        }
    }
```

##### ����������ÿ�δ���ViewHolder��ʱ��Ҫ����item�����ļ�ָ���ؼ�������������item�ļ����ˣ���Ҫ���´���ViewHolder�࣬���Խ���������Ͳ��ܵ����ĸ���item�ļ���ʲô�ؼ���ָ��ʲô�ؼ�������ViewHolder�У�SparseArray����Map���񣬶���key-value��ʽ�ģ�����Androidȴ���ʹ��SparseArray��������࣬�����ṩ�ġ��۰���Һ��������ܹ���߲���Ч�ʣ�

##### �������ViewHolder�У�ʹ��SparseArray<View>�����ݿؼ���IDΪkey,�����Ӧ�Ŀؼ�id�Ķ���

##### ���ԣ��������д�ɣ�

```xml
package com.base.commonrecycleview;

import android.graphics.Bitmap;
import android.graphics.drawable.Drawable;
import android.support.v7.widget.RecyclerView;
import android.util.SparseArray;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;

/**
 * Created by ��˧ on 2016/9/22.
 */
public class CommonRecycleViewHolder extends RecyclerView.ViewHolder {

    private static final String TAG = "CommonRecycleViewHolder.class";
    //����View�ļ���
    private SparseArray<View> mSparseArray = null;
    /**
     * �ļ�������
     */
    private View rootView;
    public CommonRecycleViewHolder(View itemView) {
        super(itemView);
        /**
         * ��ʼ��
         */
        this.mSparseArray = new SparseArray<View>();
        this.rootView = itemView;

    }



    /**
     * ����TextView
     * @param id TextView��Ӧ�ģɣ�
     * @param msgText ��ӵ�����
     */
    public void setText(int id, String msgText) {

        try {
            View view = getView(id);

            if (view != null){
                if (view instanceof TextView) {
                    //CharSequence
                    ((TextView) view).setText(""+msgText);
                }else
                    throw new ClassCastException("Current View not Convert To The TextView");

            }
        }catch (Exception e) {
            e.printStackTrace();
        }

    }


    /**
     * ����TextView
     * @param id TextView��Ӧ�ģɣ�
     * @param msgText ��ӵ�����
     */
    public void setText(int id, CharSequence msgText) {

        try {
            View view = getView(id);

            if (view != null){
                if (view instanceof TextView) {
                    ((TextView) view).setText(""+msgText);
                }else
                    throw new ClassCastException("Current View not Convert To The TextView");

            }
        }catch (Exception e) {
            e.printStackTrace();
        }

    }


    /**
     * ����drawable��ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param drawable ͼƬ��ʾ��Դ
     */
    public void setImageDrawable(int id, Drawable drawable) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageDrawable(drawable);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }

    }

    /**
     * ������Դ�ļ���ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param resource ͼƬ��ʾ��Դ
     */
    public void setImageResource(int id, int resource) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageResource(resource);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }

    }

    /**
     * ����Bitmap��ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param bitmap ͼƬ��ʾ��Դ
     */
    public void setImageBitmap(int id, Bitmap bitmap) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageBitmap(bitmap);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * ���ݿؼ���ID��ȡ����
     * @param id �ؼ�id
     * @return
     */
    public View getView(int id) {

        View view = null;
        try {

            if (mSparseArray == null)
                throw new NullPointerException("SparseArray is null");

            if (rootView == null)
                throw new NullPointerException("rootView is null");

            if (id < 0)
                throw new IllegalArgumentException("TextView id not invalidate");

            view = mSparseArray.get(id);

            if (view == null) {
                view = rootView.findViewById(id);

                if (view != null){

                    mSparseArray.put(id, view);
                }
            }
        }catch (Exception e) {
            e.printStackTrace();
        }

        return view;
    }
    /**
     * ���ü����¼��Ľӿ�
     */
    public interface SetOnViewClickListener{
        public void onViewListener(View view);
    }

    /**
     * ���ü����¼�
     * @param id
     * @param setOnViewClickListener
     */
    public void setViewListener(int id, final SetOnViewClickListener setOnViewClickListener) {

        try {

            View view = getView(id);

            if (view != null){
                view.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

                        if (setOnViewClickListener != null) {
                            setOnViewClickListener.onViewListener(view);
                        }
                    }
                });
            }
        }catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
##### �ģ�������ʹ������Դ��ͨ������ͨ��List<Object>������Adapter�ģ���ȻObject��Ӧ��ʵ�壬���ָ�����Ȼ�����ǲ���ÿһ��ʵ�嶼Ҫ����һ��Adapter�����Կ��Խ�Adapter��Ϊ���ͣ�

##### �����������������ʱ�� class MyAdapter<T>����д���Ϳ��Խ�List<T>�������

##### ���ԣ��������д�ɣ�

```xml
public abstract class CommonRecycleAdapter<T> extends RecyclerView.Adapter<CommonRecycleViewHolder> {

    /**
     * �����߼����˽���������ʹ��
     * @param holder CommonRecycleViewHolder
     * @param position ��ǰ����item��λ��
     */
    public abstract void onCommonBindViewHolder(CommonRecycleViewHolder holder, int position);
    private Context context;
    private List<T> datas;
    private LayoutInflater mLayoutInflater;
    private int layoutId;
    public  CommonRecycleAdapter(Context context, List<T> datas, int layoutId) {

        this.context = context;
        this.datas = datas;
        this.layoutId = layoutId;
        this.mLayoutInflater = LayoutInflater.from(context);
    }
```

##### ��������Ѿ�û���ˣ��Ҹ�����Ϊ�����ĸ�����ԸĽ��ģ����绹�и�λͬѧ�в�ͬ�Ľ��鶼���������������໥���������Ҳ��һ�����񣬣�������ѧϰ���������������������ɵĴ��룺
*********************
- MainActivity.class ���룺
```xml
 mProgressBar = (ProgressBar) findViewById(R.id.progress);
        mRecyclerView = (RecyclerView) findViewById(R.id.recycleview);

        LinearLayoutManager layoutManager = new LinearLayoutManager(this);
        layoutManager.setOrientation(OrientationHelper.VERTICAL);
        //����Item���ӡ��Ƴ�����
        mRecyclerView.setItemAnimator(new DefaultItemAnimator());

        mRecyclerView.setLayoutManager(layoutManager);

        /**
         * �󶨵�����ֵ�׵�����ʹ��
         */
        adapter = new CommonRecycleAdapter(this, datas, R.layout.item_layout) {
            @Override
            public void onCommonBindViewHolder(CommonRecycleViewHolder holder, final int position) {

                final AppInfo info = datas.get(position);
                holder.setImageDrawable(R.id.icons, info.appIcon);
                holder.setText(R.id.titles, info.appName);

                /**
                 * ���ü����¼�
                 */
//                holder.setViewListener(R.id.icons, new CommonRecycleViewHolder.SetOnViewClickListener() {
//                    @Override
//                    public void onViewListener(View view) {
//
//                        Log.e("MainActivity.class", ""+info.appName);
//                    }
//                });
//
//                holder.setViewListener(R.id.titles, new CommonRecycleViewHolder.SetOnViewClickListener() {
//                    @Override
//                    public void onViewListener(View view) {
//
//                        Log.e("MainActivity.class", ""+position);
//                    }
//                });

                holder.setViewListener(R.id.items, new CommonRecycleViewHolder.SetOnViewClickListener() {
                    @Override
                    public void onViewListener(View view) {

                        Log.e("MainActivity.class", "��ǰ"+info.appPackName);
                    }
                });
            }
        };


        mRecyclerView.setAdapter(adapter);
```
- CommonRecycleAdapter<T>.class ���룺
```xml
package com.base.commonrecycleview;

import android.content.Context;
import android.support.v7.widget.RecyclerView;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.ViewGroup;

import java.util.List;

/**
 * Created by ��˧ on 2016/9/22.
 */
public abstract class CommonRecycleAdapter<T> extends RecyclerView.Adapter<CommonRecycleViewHolder> {

    /**
     * �����߼����˽���������ʹ��
     * @param holder CommonRecycleViewHolder
     * @param position ��ǰ����item��λ��
     */
    public abstract void onCommonBindViewHolder(CommonRecycleViewHolder holder, int position);
    private Context context;
    private List<T> datas;
    private LayoutInflater mLayoutInflater;
    private int layoutId;
    public  CommonRecycleAdapter(Context context, List<T> datas, int layoutId) {

        this.context = context;
        this.datas = datas;
        this.layoutId = layoutId;
        this.mLayoutInflater = LayoutInflater.from(context);
    }
    @Override
    public CommonRecycleViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return new CommonRecycleViewHolder(mLayoutInflater.inflate(layoutId, parent, false));
    }

    @Override
    public void onBindViewHolder(CommonRecycleViewHolder holder, int position) {

        /**
         * ��Adapter��Ϊ�����࣬�����ṩ����ķ�����
         * ʹonBindViewHolder������д�������չʹ��
         */
        onCommonBindViewHolder(holder, position);
    }

    @Override
    public int getItemCount() {
        return datas==null?0:datas.size();
    }

    /**
     * �Ƴ���������
     */
    public void clearAllDatas() {

        if (datas != null) {
            datas.clear();
        }
    }

    /**
     * ��������
     * @param newDatas
     */
    public void addDatas(List<T> newDatas) {

        if (datas != null && newDatas != null){
            datas.addAll(newDatas);
        }
    }

    /**
     * ��������
     * @param datas
     */
    public void resetDatas(List<T> datas) {

        try {

            if (this.datas != null){
                this.datas.clear();

                if (datas != null) {
                    this.datas.addAll(datas);
                }
            }

        }catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
- CommonRecycleViewHolder.class ����
```xml
package com.base.commonrecycleview;

import android.graphics.Bitmap;
import android.graphics.drawable.Drawable;
import android.support.v7.widget.RecyclerView;
import android.util.SparseArray;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;

/**
 * Created by ��˧ on 2016/9/22.
 */
public class CommonRecycleViewHolder extends RecyclerView.ViewHolder {

    private static final String TAG = "CommonRecycleViewHolder.class";
    //����View�ļ���
    private SparseArray<View> mSparseArray = null;
    /**
     * �ļ�������
     */
    private View rootView;
    public CommonRecycleViewHolder(View itemView) {
        super(itemView);
        /**
         * ��ʼ��
         */
        this.mSparseArray = new SparseArray<View>();
        this.rootView = itemView;

    }



    /**
     * ����TextView
     * @param id TextView��Ӧ�ģɣ�
     * @param msgText ��ӵ�����
     */
    public void setText(int id, String msgText) {

        try {
            View view = getView(id);

            if (view != null){
                if (view instanceof TextView) {
                    //CharSequence
                    ((TextView) view).setText(""+msgText);
                }else
                    throw new ClassCastException("Current View not Convert To The TextView");

            }
        }catch (Exception e) {
            e.printStackTrace();
        }

    }


    /**
     * ����TextView
     * @param id TextView��Ӧ�ģɣ�
     * @param msgText ��ӵ�����
     */
    public void setText(int id, CharSequence msgText) {

        try {
            View view = getView(id);

            if (view != null){
                if (view instanceof TextView) {
                    ((TextView) view).setText(""+msgText);
                }else
                    throw new ClassCastException("Current View not Convert To The TextView");

            }
        }catch (Exception e) {
            e.printStackTrace();
        }

    }


    /**
     * ����drawable��ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param drawable ͼƬ��ʾ��Դ
     */
    public void setImageDrawable(int id, Drawable drawable) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageDrawable(drawable);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }

    }

    /**
     * ������Դ�ļ���ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param resource ͼƬ��ʾ��Դ
     */
    public void setImageResource(int id, int resource) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageResource(resource);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }

    }

    /**
     * ����Bitmap��ͼƬ
     * @param id ImageView�Ŀؼ�
     * @param bitmap ͼƬ��ʾ��Դ
     */
    public void setImageBitmap(int id, Bitmap bitmap) {

        try {

            View view = getView(id);

            if (view != null ){
                if (view instanceof ImageView) {
                    ((ImageView) view).setImageBitmap(bitmap);
                }else
                    throw new ClassCastException("Current View not Convert To The ImageView");
            }

        }catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * ���ݿؼ���ID��ȡ����
     * @param id �ؼ�id
     * @return
     */
    public View getView(int id) {

        View view = null;
        try {

            if (mSparseArray == null)
                throw new NullPointerException("SparseArray is null");

            if (rootView == null)
                throw new NullPointerException("rootView is null");

            if (id < 0)
                throw new IllegalArgumentException("TextView id not invalidate");

            view = mSparseArray.get(id);

            if (view == null) {
                view = rootView.findViewById(id);

                if (view != null){

                    mSparseArray.put(id, view);
                }
            }
        }catch (Exception e) {
            e.printStackTrace();
        }

        return view;
    }
    /**
     * ���ü����¼��Ľӿ�
     */
    public interface SetOnViewClickListener{
        public void onViewListener(View view);
    }

    /**
     * ���ü����¼�
     * @param id
     * @param setOnViewClickListener
     */
    public void setViewListener(int id, final SetOnViewClickListener setOnViewClickListener) {

        try {

            View view = getView(id);

            if (view != null){
                view.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

                        if (setOnViewClickListener != null) {
                            setOnViewClickListener.onViewListener(view);
                        }
                    }
                });
            }
        }catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

- mian_layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.base.commonrecycleview.MainActivity">


    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycleview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:visibility="gone" />


    <ProgressBar
        android:id="@+id/progress"
        style="?android:attr/progressBarStyleLarge"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:indeterminate="false"
        android:visibility="visible" />

</FrameLayout>

```

- item.layout 
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/items"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">

    <LinearLayout
        android:background="@drawable/ripple_bg"
        android:orientation="horizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageView
            android:id="@+id/icons"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="8dp"
            android:contentDescription="@string/app_name"
            android:src="@mipmap/ic_launcher" />

        <TextView
            android:id="@+id/titles"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_weight="1"
            android:gravity="center"
            android:text="@string/app_name"
            android:textColor="@android:color/black"
            android:textSize="16sp" />

    </LinearLayout>

    <View
        android:paddingTop="2dp"
        android:paddingBottom="2dp"
        android:background="@color/colorAccent"
        android:layout_width="match_parent"
        android:layout_height="1dp"></View>

</LinearLayout>
```


##### ���������ȫ�����꣬�ҽ�����Ŀʵ��Сdemonȫ������GitHub�����ˣ�����Ҫ��ͬѧ��������һ�¿�һ�£�https://github.com/gifmeryshuai/androidProject.git
##### ��Ŀ���ƣ�CommonRecycleView