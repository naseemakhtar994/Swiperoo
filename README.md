# Swiperoo Adapter

An extandable adapter which provides *swipe to delete* on your row item.

Inspired by: https://github.com/nemanja-kovacevic/recycler-view-swipe-to-delete

## Installation

#### Gradle
Add Gradle dependency:

```groovy
dependencies {
    compile 'us.belka:swiperoo-library:1.0.0'
}
```

#### Maven
```xml
<dependency>
  <groupId>us.belka</groupId>
  <artifactId>swiperoo-library</artifactId>
  <version>1.0.0</version>
  <type>pom</type>
</dependency>
```

## Usage

In the app folder you will find a working example of the library

You need to do 3 things to make the library works:

### 1. Create your ViewHolder
```java
    public class MyViewHolder extends SwiperooViewHolder<String> {

        static class Factory implements SwiperooViewHolder.Factory {

            @Override
            public SwiperooViewHolder createViewHolder(Context context, ViewGroup parent, int viewType) {
                return new MyViewHolder(from(context).inflate(YOUR_ITEM_LAYOUT, parent, false), context);
            }
        }

        public MyViewHolder(View itemView, Context context) {
            super(itemView, context);
        }

        @Override
        public void bindViewHolder(String data) {

        }
    }
```

Pay attention to the Factory class, you need to return an instance of your ViewHolder (Factory pattern)

### 2. Create your Adapter

```java
    public class MyAdapter extends SwiperooAdapter<String> {

        public MyAdapter(Context context, List<String> items, Listener listener, SwiperooViewHolder.Factory factory) {
            super(context, items, listener, factory);
        }
    }
```

### 3. Put it all togheter

```java
    mSwiperooRecyclerView.setLayoutManager(new LinearLayoutManager(this));
    MyAdapter adapter = new MyAdapter(this, items, this, new MyViewHolder.Factory());

    mSwiperooRecyclerView.setAdapter(adapter);

    adapter.addSupportToSwipeToDelete(this, mSwiperooRecyclerView);
```

You can use "this" as third parameter in the Adapter or you can directly pass in an implementation of the Listener, both ways you will implement the interface to handle item delete

## Listeners

```java
@Override
    public void onItemDeleted(String item) {
       ///Do your stuff with the deleted item
    }
```

## Pay attention

Your item layout container must be a **Relative Layout**, otherwise the Holder will throw you a NotSupportedException

