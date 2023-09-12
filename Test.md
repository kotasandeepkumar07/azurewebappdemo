
###

|  Python |  C++ |
| ------------ | ------------ |
|  .clip(0.0000001, 1)  | cv:max(inputImg, 0.0000001, outputImg); <br> cv:min(inputImg, 1.0, outputImg); |
|  im_log = -np.log(img)  |  cv::Mat im_log; <br>cv::log(im, im_log); <br>im_log * = -1.f; |
| img_grayscale = cv2.cvtColor(img.data, cv2.COLOR_BGR2GRAY)			 | cv::cvtColor(input, input, cv::COLOR_BGR2GRAY)  |
| cv2.createCLAHE(clipLimit=1000.0, tileGridSize=(tile_size, tile_size))		|  cv::createCLAHE(1000.0, cv::Size{ tile_size, tile_size }) |
| area_mask[~img.segmentation[RegionType.FACE].mask] = 0  					|   area_mask_image.forEach(uint8_t)([&face_mask] uint8_t &point, const int *position) { <br> constexpr auto kSkin = 2;<br> auto face_mask_value = face_mask.at<uint8_t>(position);  <br> if (face_mask_value != kSkin) point = 0;}); |
| im_log.T.reshape(3, -1, order='F') <br> <br>This converts [[[RGB],[RGB],[RGB],[RGB],...],[...],...] to [[RRRR...],[GGGG...],[BBBB...]] |    std::vector<cv::Mat> channels; <br> cv::split(im_log, channels); <br> auto const image_size_bytes = image_pixel_count * sizeof(float); <br> std::memcpy(output.data, channels[0].data, image_size_bytes);  <br> std::memcpy(output.data + image_size_bytes, channels[1].data, image_size_bytes);  <br> std::memcpy(output.data + 2 * image_size_bytes, channels[2].data, image_size_bytes); |
| low_thresh = np.nanpercentile(l, 20)  | float low_threshold;  <br> float index = (20.0 / 100.0) * (vec_from_mat.size() + 1);  <br> if (std::ceil(index) == index)<br>  {  low_threshold = vec_from_mat[static_cast<int>(index)];  } <br> else {  low_threshold = vec_from_mat[(static_cast<int>(index) + static_cast<int>(index + 1)) / 2];   } | 
|  median = np.nanmedian(l) |     std::nth_element(vec_from_mat.begin(), vec_from_mat.begin() + vec_from_mat.size() / 2, <br> vec_from_mat.end()); <br>  float median = vec_from_mat[vec_from_mat.size() / 2];

