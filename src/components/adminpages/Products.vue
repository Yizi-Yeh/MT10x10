<template>
<div class="container-fulid">
  <div class="text-right">
      <button class="btn btn-sm bg-dark rounded"  data-toggle="modal" data-target="#productModal" @click="openModal(true)">建立新的行程</button>
  </div>

    <table class="table mt-4 table-sm">
      <thead>
        <tr class="text-center">
          <th >分類</th>
          <th >名稱</th>
          <!-- <th >地點</th> -->
          <th >價格</th>
          <th >時間</th>
          <th >說明</th>
          <!-- <th >費用包含</th> -->
          <!-- <th >注意事項</th>
          <th >報名須知</th>
          <th >日程</th>
          <th >行程內容</th>
          <th >餐食日程</th>
          <th >餐食</th> -->
          <th >圖片</th>
          <th >上架</th>
          <th >  編輯/刪除</th>
          <th >開團</th>
        </tr>
      </thead>
      <tbody  class="text-center">
        <tr v-for="(item) in plans" :key="item._id">
          <td>{{ item.category }}</td>
          <td class="long-text">{{ item.title }}</td>
          <!-- <td class="long-text">{{ item.site }}</td> -->
          <td class="long-text">NT${{ item.cost }}</td>
          <td class="long-text">{{ item.time }}</td>
          <td class="long-text" >{{ item.introduction}}</td>
          <!-- <td class="long-text">{{ item.costinclude}}</td> -->
          <!-- <td class="long-text">{{ item.attention}}</td>
          <td class="long-text">{{ item.noteForJoin}}</td> -->
          <!-- <td class="long-text">{{ item.schedule[0].dateTime}}</td>
          <td class="long-text">{{ item.schedule[0].content}}</td>
          <td class="long-text">{{ item.meal[0].mealdateTime}}</td>
          <td class="long-text">{{ item.meal[0].mealcontent}}</td> -->
          <td v-if="item.images[0].imgUrl !== undefined"><img :src= item.images[0].imgUrl width="100"></td>
          <td v-else><img :src="form.file" width="100" ></td>
          <td>
            <span v-if="item.is_enabled" class="text-success">啟用</span>
            <span v-else>未啟用</span>
          </td>
          <td>
        <button class="btn btn-outline-success ml-2 mr-2 rounded btn-sm" @click="openModal(false, item)">編輯</button>
        <button class="btn btn-outline-danger rounded btn-sm" @click="delProducts(item._id)">刪除</button>
          </td>
          <td>
        <button class="btn btn-outline-dark rounded btn-sm" @click="createPlan(item._id)">開團</button>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- Modal -->
<div class="modal fade" id="productModal" tabindex="-1" role="dialog">
  <div class="modal-dialog modal-lg" role="document">
    <div class="modal-content border-0">
      <div class="modal-header bg-dark text-white">
          <h5 class="modal-title" id="exampleModalLabel">
              <span>新增行程</span>
            </h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
            <div class="row">
              <div class="col-sm-4">
                <div class="form-group">
                  <label for="image">輸入圖片網址</label>
                  <input type="text" class="form-control" id="imgUrl"
                    v-model="form.imgUrl"
                    placeholder="請輸入圖片連結">
                </div>
                <div class="form-group">
                  <label for="customFile">或 上傳圖片
                  </label>
                  <input type="file" id="file" class="form-control" name="file"
                    ref="files" 
                    >
                </div>
              </div>
              <div class="col-sm-8">
                <div class="form-group">
                  <label for="category">活動分類</label>
                  <input type="text" class="form-control" id="category"
                    v-model="form.category"
                    placeholder="請輸入活動分類">
                </div>
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <label for="title">活動標題</label>
                    <input type="text" class="form-control" id="title"
                      v-model="form.title"
                      placeholder="請輸入活動標題">
                  </div>
                  <div class="form-group col-md-6">
                    <label for="site">活動地點</label>
                    <input type="text" class="form-control" id="site"
                      v-model="form.site"
                      placeholder="請輸入地點">
                  </div>
                </div>

                <div class="form-row">
                  <div class="form-group col-md-6">
                  <label for="cost">活動成本</label>
                    <input type="text" class="form-control" id="cost"
                      v-model="form.cost"
                      placeholder="請輸入活動成本">
                  </div>
                  <div class="form-group col-md-6">
                    <label for="time">活動時間</label>
                    <input type="text" class="form-control" id="time"
                      v-model="form.time"
                      placeholder="請輸入活動時間">
                  </div>
                </div>
                <hr>

                <div class="form-group">
                  <label for="introduction">活動說明</label>
                  <textarea type="text" class="form-control" id="introduction"
                    v-model="form.introduction"
                    placeholder="請輸入活動說明"></textarea>
                </div>
                <div class="form-group">
                  <label for="costinclude">費用包含</label>
                  <textarea type="text" class="form-control" id="costinclude"
                    v-model="form.costinclude"
                    placeholder="請輸入費用包含事項"></textarea>
                </div>
                <div class="form-group">
                  <label for="attention">注意事項</label>
                  <textarea type="text" class="form-control" id="attention"
                    v-model="form.attention"
                    placeholder="請輸入注意事項"></textarea>
                </div>

                 <div class="form-group">
                  <label for="noteForJoin">報名須知</label>
                  <textarea type="text" class="form-control" id="noteForJoin"
                    v-model="form.noteForJoin"
                    placeholder="請輸入報名須知"></textarea>
                </div>

                <div class="form-group">
                  <label for="schedule">行程安排</label>
                  <textarea type="text" class="form-control mb-3" id="dateTime"
                    v-model="form.schedule[0].dateTime"
                    placeholder="請輸入行程安排日程"></textarea>

                    <textarea type="text" class="form-control" id="content"
                    v-model="form.schedule[0].content"
                    placeholder="請輸入行程安排內容"></textarea>
                </div>

                <!-- <div class="form-group">
                  <label for="schedule">行程安排</label>
                  <textarea type="text" class="form-control mb-3" id="dateTime"
                    v-model="form.schedule[1].dateTime"
                    placeholder="請輸入行程安排日程"></textarea>

                    <textarea type="text" class="form-control" id="content"
                    v-model="form.schedule[1].content"
                    placeholder="請輸入行程安排內容"></textarea>
                </div>

                <div class="form-group">
                  <label for="schedule">行程安排</label>
                  <textarea type="text" class="form-control mb-3" id="dateTime"
                    v-model="form.schedule[2].dateTime"
                    placeholder="請輸入行程安排日程"></textarea>

                    <textarea type="text" class="form-control" id="content"
                    v-model="form.schedule[2].content"
                    placeholder="請輸入行程安排內容"></textarea>
                </div> -->

                
                <div class="form-group">
                  <label for="meal">餐食安排</label>
                  <textarea type="text" class="form-control mb-3" id="mealdateTime"
                    v-model="form.meal[0].mealdateTime"
                    placeholder="餐食安排請輸入日程"></textarea>

                    <textarea type="text" class="form-control" id="mealcontent"
                    v-model="form.meal[0].mealcontent"
                    placeholder="餐食安排請輸入內容"></textarea>
                </div>
<!-- 
                <div class="form-group">
                  <label for="meal">餐食安排</label>
                  <textarea type="text" class="form-control mb-3" id="mealdateTime"
                    v-model="form.meal[1].mealdateTime"
                    placeholder="餐食安排請輸入日程"></textarea>

                    <textarea type="text" class="form-control" id="mealcontent"
                    v-model="form.meal[1].mealcontent"
                    placeholder="餐食安排請輸入內容"></textarea>
                </div>

                <div class="form-group">
                  <label for="meal">餐食安排</label>
                  <textarea type="text" class="form-control mb-3" id="mealdateTime"
                    v-model="form.meal[2].mealdateTime"
                    placeholder="餐食安排請輸入日程"></textarea>

                    <textarea type="text" class="form-control" id="mealcontent"
                    v-model="form.meal[2].mealcontent"
                    placeholder="餐食安排請輸入內容"></textarea>
                </div> -->
                
                <div class="form-group">
                  <div class="form-check">
                    <input class="form-check-input" type="checkbox"
                      v-model="form.is_enabled"
                      :true-value="true"
                      :false-value="false"
                      id="is_enabled">
                    <label class="form-check-label" for="is_enabled">
                      是否上架
                    </label>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn  btn-sm rounded btn-outline-secondary" data-dismiss="modal">取消</button>
            <button type="button" class="btn btn-sm rounded btn-dark" @click="addProduct()">確認</button>
          </div>
        </div>
      </div>
    </div>
</div>
</template>
<script>
import $ from 'jquery';
import Axios from 'axios'
export default {
    data() {
        return {
            plans:[],
            form:{
              images:[{
                description: '',
                file:'',
                imgUrl: '',
              }],
              schedule:[{
                dateTime: '',
                content: '',
              },
              {
                dateTime: '',
                content: '',
              },{
                dateTime: '',
                content: '',
              }],
              meal:[{
               mealdateTime: '',
               mealcontent: ''
              },
              {
               mealdateTime: '',
               mealcontent: ''
              },
              {
               mealdateTime: '',
               mealcontent: ''
              }],
            },
            isNew: false,
        }
    },
    methods: {
      // 取得所有產品
        getProducts() {
        const api = `${process.env.VUE_APP_API}`+ '/products'
        const vm = this;
        vm.isLoading = true;
        Axios.get(api).then((response) => {
        // console.log(response.data)
        vm.isLoading = false;
        vm.plans = response.data.result
        console.log(response.data.result)
        })
        },

        getProductsId(id) {
        const api = `${process.env.VUE_APP_API}`+ '/'
        const vm = this;
        Axios.post(api,{p_id}).then((response) => {
        // console.log(response.data)
        const index = vm.plans.findIndex( item => {
          return item._id === id 
          }) 
        vm.plansId = response.data.result[index]._id
        console.log(vm.plansId)
        })
        },
        // 取得單一產品
        getProduct() {
        const id = this.$route.params.id;
        const api = `${process.env.VUE_APP_API}` + '/products/' + id
        const vm = this;
        vm.$http.get(api).then((response) => {
        if(response.data.success){
        vm.plan = response.data.result
          } 
        })
        },
 
        // 在products中找到id並刪除產品
        delProducts(id) {
        const api = `${process.env.VUE_APP_API}`+ '/products/' + id
        const vm = this;
        vm.$http.delete(api).then((response) => {
          const index = vm.plans.findIndex( item => {
          return item._id === id 
          }) 
          // splice(index,1) 在index位置處刪除一個元素
          this.plans.splice(index,1)
          })
        .catch(error => {
          alert(error.response.data.message)
        }) 
        },    
        //修改行程 
        addProduct() {
        let api = `${process.env.VUE_APP_API}`+ '/products'
        let httpMethod = 'post';
        const vm = this;
        if (!vm.isNew) {
          api = `${process.env.VUE_APP_API}`+ '/products/' + `${vm.form._id}`
          httpMethod = 'put'
        } 
        this.$http[httpMethod](api, vm.form).then((response) => {
        if(response.data.succuss) {
          // vm.plans.push(response.data.result)
          $('#productModal').modal('hide')
          vm.getProducts()
        } else {
            vm.getProducts();
          $('#productModal').modal('hide');
        } 
    })
    },
      // 上傳圖片
      updateImg() {
      // Vue實體中圖片置放位置
      const updated = this.$refs.files.files[0];
      const vm = this;
      // 使用new FormData 操作表單
      const fd = new FormData();
      // 然後透過 append 加入欄位 ，傳入圖片
      fd.append('file', updated);
      const api = `${process.env.VUE_APP_API}`+ '/products';
      // post fd本身，並設置表單名稱
      this.$http.post(api, fd, { headers: {
          'Content-Type': 'multipart/form-data',
        },
      }).then((response) => {
        // console.log(response.data);
        if (response.data.succuss) {
        vm.$set(vm.form,'file',process.env.VUE_APP_API + '/products/file/' + response.data.result.images[0].file)
        } console.log(vm.form.file)
      });
    },
      getImgUrl () {
      return process.env.VUE_APP_API + '/products/file/' + response.data.result.images[0].file
      },
      openModal(isNew, item) {
      if (isNew) {
        this.form = {};
        this.isNew = true;
      } else {
        // 將item值寫入空物件
        this.form = Object.assign({}, item);
        this.isNew = false;
      }
        $('#productModal').modal('show');
      },
      getProductsInfo() {
        this.$store.dispatch('getProductsInfo');
      },
      createPlan (id) {  
        const api = `${process.env.VUE_APP_API}`+ '/newplans'
        Axios.post(api,{p_id:id}).then((response) => {
          if(response.data.succuss){
                  this.$router.push('/admin/newplans')
            // this.$router.push('/admin/newplans?product=' + id)
          } 
        })
      }
    },
    created() {
        this.getProducts()
        this.getProduct()
    }
}
</script>
<style lang="scss" scoped>
table{
   table-layout: fixed;
}
tr{
  white-space:nowrap;
}
.long-text {white-space:nowrap!important;overflow:hidden!important;text-overflow: ellipsis!important }

.btn-outline-success{
  border: 2px solid #c5d1cc;
  color:#c5d1cc ;
}


</style>