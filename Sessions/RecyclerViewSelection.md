# RecyclerViewSelection
[Youtube](https://www.youtube.com/watch?time_continue=1271&v=jdKUm8tGogw)

```
dependencies {
  implementation "androidx.recyclerview:recyclerview-selection1.0.0-alpha"
}
```

Adapter と LayoutManager は今まで通り

RecyclerView.Adapter に `getItemId` を生やす(例では position.toLong にキャスト)

```
val keyProvider = StableIdKeyProvider(recyclerView)


mSelectionTracker = SelectionTracker.Builder(
  "demo",
  recyclerView,
  keyProvider,
  MyDetailsLookup(recyclerView), StorageStrategy.createLongStorage()).build()
```

```
class DemoDetailsLookup(val recyclerView: RecyclerView) : ItemDetailsLookup<Long>() {
  override fun getItemDetails(e: MotionEvent): ItemDetailsLookup.ItemDetails<Long>? {
    val view = recyclerView.findChildViewUnder(event.x, event.y) ?: return null

    val holder = recyclerView.getChildViewHolder(view)
    if (holder is HogeViewHolder) {
      override fun getPosition(): Int = holder.adapterPosition
      override fun getSelectionKey(): Long? = holder.itemId
    }
  }
}
```

Adapter
```
override fun onBindViewHolder(いつもの) {
  val key = getItemId(position)
  val selected = selectionTracker.isSelected(key)
  holder.label.apply {
    …
  }
}
```

TextView の background に selector をセットする
`android:state_activated` のパラメータを使用する


## ListAdapter の Diff
`DiffUtil.ItemCallback` でリストの差分判定

```
DIFF_CALLBACK は DiffUtil.ItemCallback の object

class MyAdapter(): ListAdapter<User, UserViewHolder>(DIFF_CALLBACK) {
  override fun onBindViewHolder(いつもの) {
    val user = getItem(position)
    …
  }
}
```

`myAdapter.submitList(list)`

`AsyncListDiffer` というのも追加されている
