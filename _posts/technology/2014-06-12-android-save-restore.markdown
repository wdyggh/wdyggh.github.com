---
layout: post
category: "android"
title:  "Android数据保存与恢复"
tags: [数据恢复]
---
Android onSaveInstanceState onRestoreInstanceState的作用不必多说，使用时要稍注意一下。  
示例中可以看到，没在onRestoreInstanceState方法中直接恢复数据，这是因为Activity重新onCreate时，数据可能还没恢复完毕，onCreate就开始使用data了，从而导致异常（特别在savedInstanceState中要恢复很多数据时）。  

示例代码：
{% highlight java %}
	private String data="some user data";
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		if(savedInstanceState!=null) {//如果有数据被需恢复，onRestoreInstanceState会被触发，并将savedInstanceState传递到onCreate
			Log.d(TAG,"onRestoreInstanceState is not null...");
			data=savedInstanceState.getString("data");
		}
		
		//tv.setText(data);
	}

	@Override
	protected void onSaveInstanceState(Bundle outState) {
		super.onSaveInstanceState(outState);
		outdate.putString("data", data);
	}

	@Override
	protected void onRestoreInstanceState(Bundle savedInstanceState) {//savedInstanceState会传递到onCreate，在onCreate中恢复
		super.onRestoreInstanceState(savedInstanceState);
		//data=savedInstanceState.getString("data");//不在这里用data=savedInstanceState.getString("data");直接来恢复。
	}
{% endhighlight %}

参考文章：<http://blog.csdn.net/lamp_zy/article/details/10156369>

