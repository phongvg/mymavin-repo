<script>
/**
 * News-Dashboard component
 */
export default {
  head() {
    return {
      title: `Trang quản trị Tin tức | My Mavin`,
    };
  },
  middleware: "router-auth",
  data() {
    return {
      title: "Xin chào!",
      items: [
        {
          text: "My Mavin",
        },
        {
          text: "Trang quản trị",
        },
        {
          text: "Tin tức",
          active: true,
        },
      ],
      productData: [],
      totalRows: 1,
      currentPage: 1,
      perPage: 10,
      pageOptions: [10, 25, 50, 100],
      filter: null,
      filterOn: [],
      sortBy: "age",
      sortDesc: false,
      fields: [
        {
          key: "check",
          label: "",
        },
        {
          key: "Product",
          label: "Bài viết",
        },
        {
          key: "category",
          label: "Chủ đề",
        },
        {
          key: "date",
          label: "Ngày tạo",
          sortable: true,
        },
        {
          key: "createdBy",
          label: "Người tạo",
        },
        {
          key: "Rating",
          label: "Rating",
          sortable: true,
        },
        {
          key: "quality",
          label: "Lượt bình luận",
          sortable: true,
        },
        {
          key: "status",
          label: "Trạng thái",
          sortable: true,
        },
        "action",
      ],
    };
  },
  created() {
    setTimeout(() => {
      this.productData = [
        {
          id: 1,
          image: require("~/assets/images/news/news-1.png"),
          name: "Mavin tham gia Hội nghị thượng đỉnh liên kết Doanh nghiệp Limitless 2022 của World Vision",
          rating: "4.9",
          category: "Tin Mavinex",
          date: "02/07/2020",
          createdBy: "Admin",
          quality: 112,
          status: "Active",
        },
        {
          id: 2,
          image: require("~/assets/images/news/news-2.png"),
          name: "Mavin được trao giải “Doanh nghiệp tiên phong Đông Nam Á” từ SAP",
          rating: "3.1",
          category: "Tin MavinFood",
          date: "02/06/2020",
          createdBy: "Minh - Mavinex",
          quality: 60,
          status: "Active",
        },
        {
          id: 3,
          image: require("~/assets/images/news/news-3.png"),
          name: "Mavin và Fish&Co (Cameroon) hợp tác nuôi trồng thủy sản bền vững",
          rating: "4.3",
          category: "Tin Cailay",
          date: "02/03/2020",
          createdBy: "Thu - MavinFood",
          quality: 58,
          status: "Pending",
        },
        {
          id: 4,
          image: require("~/assets/images/news/news-4.png"),
          name: "Mavin Feed 2022: Thích ứng nhanh với tình hình mới",
          rating: "4.9",
          category: "Tin Cailay",
          date: "02/04/2020",
          createdBy: "Trang - Cailay",
          quality: 98,
          status: "Active",
        },
        {
          id: 5,
          image: require("~/assets/images/news/news-5.png"),
          name: "Chính thức vận hành Hệ thống Đào tạo trực tuyến E-learning",
          rating: "2.5",
          category: "Tin Mavinex",
          date: "02/05/2020",
          createdBy: "Minh - Mavinex",
          quality: 38,
          status: "Deactive",
        },
      ];
    }, 100);
  },
  computed: {
    /**
     * Total no. of records
     */
    rows() {
      return this.productData.length;
    },
  },
  mounted() {
    // Set the initial number of items
    this.totalRows = this.items.length;
  },
  methods: {
    /**
     * Search the table data with search input
     */
    onFiltered(filteredItems) {
      // Trigger pagination to update the number of buttons/pages due to filtering
      this.totalRows = filteredItems.length;
      this.currentPage = 1;
    },
  },
};
</script>

<template>
  <div>
    <PageHeader :title="title" :items="items" />
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-body">
            <div class="row mb-2">
              <div class="col-sm-6">
                <nuxt-link to="/news/create" class="btn btn-success mb-2"
                  ><i class="mdi mdi-plus-circle mr-1"></i>Tạo bài viết
                </nuxt-link>
                <nuxt-link to="/news/create" class="btn btn-danger mb-2"
                  ><i class="mdi mdi-checkbox-marked-circle mr-1"></i>Duyệt
                  nhanh
                </nuxt-link>
              </div>

              <!-- end col-->
            </div>
            <div class="row mb-2">
              <div class="col-sm-6 col-md-6">
                <div id="tickets-table_length" class="dataTables_length">
                  <label
                    style="white-space: nowrap"
                    class="d-inline-flex align-items-center"
                  >
                    Hiển thị&nbsp;
                    <b-form-select
                      v-model="perPage"
                      size="sm"
                      :options="pageOptions"
                    ></b-form-select
                    >&nbsp;bài viết
                  </label>
                </div>
              </div>
              <!-- Search -->
              <div class="col-sm-6 col-md-6">
                <div
                  id="tickets-table_filter"
                  class="dataTables_filter text-md-right"
                >
                  <label
                    style="white-space: nowrap"
                    class="d-inline-flex align-items-center"
                  >
                    Tìm kiếm:
                    <b-form-input
                      v-model="filter"
                      type="search"
                      placeholder="Tìm kiếm..."
                      class="form-control form-control-sm ml-2"
                    ></b-form-input>
                  </label>
                </div>
              </div>
              <!-- End search -->
            </div>
            <!-- Table -->
            <div class="table-responsive mb-0">
              <b-table
                table-class="table table-centered w-100"
                thead-tr-class="bg-light"
                :items="productData"
                :fields="fields"
                responsive="sm"
                :per-page="perPage"
                :current-page="currentPage"
                :sort-by.sync="sortBy"
                :sort-desc.sync="sortDesc"
                :filter="filter"
                :filter-included-fields="filterOn"
                @filtered="onFiltered"
              >
                <template v-slot:cell(check)="data">
                  <div class="custom-control custom-checkbox text-center">
                    <input
                      type="checkbox"
                      class="custom-control-input"
                      :id="`contacusercheck${data.item.id}`"
                    />
                    <label
                      class="custom-control-label"
                      :for="`contacusercheck${data.item.id}`"
                    ></label>
                  </div>
                </template>

                <template v-slot:cell(Product)="data">
                  <!-- <img
                    v-if="data.item.image"
                    :src="data.item.image"
                    alt=""
                    class="rounded mr-3"
                    height="48"
                  /> -->
                  <div
                    v-if="!data.item.image"
                    class="avatar-xs d-inline-block mr-2"
                  >
                    <div
                      class="avatar-title bg-soft-primary rounded-circle text-primary"
                    >
                      <i class="mdi mdi-account-circle m-0"></i>
                    </div>
                  </div>
                  <h5 class="m-0 d-inline-block align-middle">
                    <a href="#" class="text-dark">{{ data.item.name }}</a>
                  </h5>
                </template>
                <template v-slot:cell(createdBy)="data">
                  {{ data.item.createdBy }}
                </template>
                <template v-slot:cell(status)="data">
                  <span
                    class="badge badge-soft-success"
                    :class="{
                      'badge-soft-danger': data.item.status === 'Deactive',
                      'badge-soft-warning': data.item.status === 'Pending',
                    }"
                    >{{ data.item.status }}</span
                  >
                </template>
                <template v-slot:cell(rating)="data">
                  <span
                    class="badge"
                    :class="{
                      'badge-success': data.item.rating >= 4,
                      'badge-danger': data.item.rating < 3,
                      'badge-warning':
                        data.item.rating > 3 && data.item.rating < 4,
                    }"
                    ><i class="mdi mdi-star"></i> {{ data.item.rating }}</span
                  >
                </template>
                <template v-slot:cell(action)="data">
                  <ul class="list-inline table-action m-0">
                    <li class="list-inline-item">
                      <nuxt-link
                        :to="`/news/preview/${data.item.id}`"
                        class="action-icon"
                      >
                        <i class="mdi mdi-eye"></i
                      ></nuxt-link>
                    </li>
                    <li class="list-inline-item">
                      <nuxt-link
                        :to="`/news/news-details/${data.item.id}`"
                        class="action-icon"
                      >
                        <i class="mdi mdi-square-edit-outline"></i
                      ></nuxt-link>
                    </li>
                    <li class="list-inline-item">
                      <a href="javascript:void(0);" class="action-icon">
                        <i class="mdi mdi-delete"></i
                      ></a>
                    </li>
                  </ul>
                </template>
              </b-table>
            </div>
            <div class="row">
              <div class="col">
                <div
                  class="dataTables_paginate paging_simple_numbers float-right"
                >
                  <ul class="pagination pagination-rounded">
                    <!-- pagination -->
                    <b-pagination
                      v-model="currentPage"
                      :total-rows="rows"
                      :per-page="perPage"
                    ></b-pagination>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- end col -->
    </div>
  </div>
</template>
