<script>
import vue2Dropzone from "vue2-dropzone";
import { productData } from "../data";

/**
 * Task-detail component
 */
export default {
  head() {
    return {
      title: `${this.title} | My Mavin`,
    };
  },
  components: {
    vueDropzone: vue2Dropzone,
  },
  asyncData({ params }) {
    const productDetail = productData.find(
      (user) => String(user.id) === params.id
    );
    return {
      productDetail,
    };
  },
  data() {
    return {
      title: "Xem trước bài viết",
      items: [
        {
          text: "My Mavin",
          href: "/",
        },
        {
          text: "Quản trị",
          href: "/",
        },
        {
          text: "Tin tức",
          active: true,
        },
      ],
      dropzoneOptions: {
        url: "https://httpbin.org/post",
        thumbnailWidth: 150,
        maxFilesize: 0.5,
        headers: {
          "My-Awesome-Header": "header value",
        },
        previewTemplate: this.template(),
      },
    };
  },
  methods: {
    template: function () {
      return ` <div class="dropzone-previews mt-3">
            <div class="card mt-1 mb-0 shadow-none border">
                <div class="p-2">
                    <div class="row align-items-center">
                        <div class="col-auto">
                            <img data-dz-thumbnail src="#" class="avatar-sm rounded bg-light" alt="">
                        </div>
                        <div class="col pl-0">
                            <a href="javascript:void(0);" class="text-muted font-weight-bold" data-dz-name></a>
                            <p class="mb-0" data-dz-size></p>
                        </div>
                        <div class="col-auto">
                            <!-- Button -->
                            <a href="" class="btn btn-link btn-lg text-muted" data-dz-remove>
                                <i class="fe-x"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        `;
    },
  },
  middleware: "router-auth",
};
</script>

<template>
  <div>
    <PageHeader :title="title" :items="items" />

    <div class="row">
      <div class="col-lg-12">
        <div class="card">
          <div class="card-body">
            <!-- <p class="text-primary">#MN2048</p> -->
            <nuxt-link to="#" class="btn btn-danger mb-2"
              ><i class="mdi mdi-checkbox-marked-circle mr-1"></i>Duyệt tin
            </nuxt-link>
            <h4 class="mb-1">{{ productDetail.name }}</h4>
            <!-- <p class="text-muted mb-1">
              Em ơi đừng khóc bóng tối trước mắt sẽ bắt em đi. Em ơi đừng lo em
              ơi đừng cho tương lai vụt tắt.
            </p> -->

            <div class="text-muted">
              <div class="row">
                <!-- <div class="col-lg-4 col-sm-6">
                  <div class="media mt-3">
                    <div class="mr-2 align-self-center">
                      <i class="ri-hashtag h2 m-0 text-muted"></i>
                    </div>
                    <div class="media-body overflow-hidden">
                      <p class="mb-1">Task ID</p>
                      <h5 class="mt-0 text-truncate">#MN2048</h5>
                    </div>
                  </div>
                </div> -->
                <div class="col-lg-6 col-sm-6">
                  <div class="media mt-3">
                    <div class="mr-2 align-self-center">
                      <img
                        src="~/assets/images/users/avatar-2.jpg"
                        alt
                        class="avatar-sm rounded-circle"
                      />
                    </div>
                    <div class="media-body overflow-hidden">
                      <p class="mb-1">Tác giả</p>
                      <h5 class="mt-0 text-truncate">Darnell McCormick</h5>
                    </div>
                  </div>
                </div>
                <div class="col-lg-6 col-sm-6">
                  <div class="media mt-3">
                    <div class="mr-2 align-self-center">
                      <i class="ri-calendar-event-line h2 m-0 text-muted"></i>
                    </div>
                    <div class="media-body overflow-hidden">
                      <p class="mb-1">Ngày tạo</p>
                      <h5 class="mt-0 text-truncate">
                        {{ productDetail.date }}
                      </h5>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <div class="mt-4">
              <div>
                <h5>Nội dung:</h5>
                <p class="text-muted">
                  Việc thực hiện mục tiêu về một thế giới không còn nạn đói, nơi
                  an ninh lương thực được đảm bảo, dinh dưỡng được cải thiện và
                  nông nghiệp bền vững được thúc đẩy vào năm 2030 ngày càng trở
                  nên khó khăn hơn. Trong năm 2021 vừa qua, gần 828 triệu người
                  bị đói trên toàn cầu. Cùng với chiến tranh, biến đổi khí hậu,
                  và đại dịch COVID-19, con đường chấm dứt đói nghèo dường như
                  còn rất xa.
                </p>
                <div class="mt-3">
                  <h5>Tags:</h5>
                  <div>
                    <a href="#" class="badge badge-soft-primary p-1 m-1"
                      >Mavin</a
                    >
                    <a href="#" class="badge badge-soft-primary p-1 m-1">Pig</a>
                    <a href="#" class="badge badge-soft-primary p-1 m-1"
                      >Food</a
                    >
                    <a href="#" class="badge badge-soft-primary p-1 m-1"
                      >Fish</a
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card">
          <div class="card-body">
            <!-- end dropdown-->
            <h5 class="header-title mb-3">Ảnh đại diện</h5>

            <div class="row">
              <div class="col-md-12">
                <div>
                  <div>
                    <img
                      v-if="productDetail.image"
                      :src="productDetail.image"
                      alt=""
                      class="rounded mr-3"
                      height="111"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-lg-12">
        <div class="card">
          <div class="card-body">
            <div class="float-right">
              <select class="custom-select custom-select-sm">
                <option selected>Mới nhất</option>
                <option value="1">Tất cả bình luận</option>
                <option value="2">Cũ nhất</option>
                <!-- <option value="3">Low to High</option> -->
              </select>
            </div>
            <!-- end dropdown-->

            <h4 class="mb-4 mt-0 font-16">Bình luận (51)</h4>

            <div class="clerfix"></div>

            <div class="media">
              <img
                class="mr-2 rounded-circle"
                src="~/assets/images/users/avatar-3.jpg"
                alt="Generic placeholder image"
                height="32"
              />
              <div class="media-body">
                <h5 class="mt-0">
                  Barry Gould
                  <small class="text-muted float-right">5 giờ trước</small>
                </h5>
                <nuxt-link to="/news/create" class="text-muted float-right"
                  ><i class="mdi mdi-delete mr-1"></i>Xóa
                </nuxt-link>
                Tin chuẩn chưa anh?
                <br />
                <a
                  href="javascript: void(0);"
                  class="text-muted font-13 d-inline-block mt-2"
                >
                  <i class="mdi mdi-reply"></i> Trả lời
                </a>

                <div class="media mt-3">
                  <a class="pr-2" href="#">
                    <img
                      src="~/assets/images/users/avatar-4.jpg"
                      class="rounded-circle"
                      alt="Generic placeholder image"
                      height="32"
                    />
                  </a>
                  <div class="media-body">
                    <h5 class="mt-0">
                      Louis Hill
                      <small class="text-muted float-right">3 giờ trước</small>
                    </h5>
                    <nuxt-link to="/news/create" class="text-muted float-right"
                      ><i class="mdi mdi-delete mr-1"></i>Xóa
                    </nuxt-link>
                    Chuẩn em nhé!
                    <br />
                    <a
                      href="javascript: void(0);"
                      class="text-muted font-13 d-inline-block mt-2"
                    >
                      <i class="mdi mdi-reply"></i> Trả lời
                    </a>
                  </div>
                </div>
              </div>
            </div>

            <div class="media mt-3">
              <img
                class="mr-2 rounded-circle"
                src="~/assets/images/users/avatar-5.jpg"
                alt="Generic placeholder image"
                height="32"
              />
              <div class="media-body">
                <h5 class="mt-0">
                  Aaron Wilson
                  <small class="text-muted float-right">1 ngày trước</small>
                </h5>
                <nuxt-link to="/news/create" class="text-muted float-right"
                  ><i class="mdi mdi-delete mr-1"></i>Xóa
                </nuxt-link>
                Bạn Chỉnh ơi, bạn đang cmt một câu mà anh rất không thích nhé.
                <br />
                <a
                  href="javascript: void(0);"
                  class="text-muted font-13 d-inline-block mt-2"
                >
                  <i class="mdi mdi-reply"></i> Trả lời
                </a>
              </div>
            </div>

            <div class="text-center mt-2">
              <a href="javascript:void(0);" class="text-danger">
                <i class="mdi mdi-spin mdi-loading mr-1"></i> Xem thêm
              </a>
            </div>

            <div class="border rounded mt-4">
              <form action="#" class="comment-area-box">
                <textarea
                  rows="3"
                  class="form-control border-0 resize-none"
                  placeholder="Your comment..."
                ></textarea>
                <div
                  class="p-2 bg-light d-flex justify-content-between align-items-center"
                >
                  <div>
                    <a href="#" class="btn btn-sm px-1 btn-light">
                      <i class="mdi mdi-upload"></i>
                    </a>
                    <a href="#" class="btn btn-sm px-1 btn-light">
                      <i class="mdi mdi-at"></i>
                    </a>
                  </div>
                  <button type="submit" class="btn btn-sm btn-success">
                    <i class="uil uil-message mr-1"></i>Đăng
                  </button>
                </div>
              </form>
            </div>
            <!-- end .border-->
          </div>
          <!-- end card-body-->
        </div>
        <!-- end card-->
      </div>
    </div>
    <!-- end row -->

    <!-- file preview template -->
  </div>
</template>
