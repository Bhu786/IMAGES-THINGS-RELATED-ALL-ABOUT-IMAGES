# IMAGES-THINGS-RELATED-ALL-ABOUT-IMAGES

  {/* Multiple Image Input */}
          <input
            type="file"
            name="featured_image"
            multiple
            onChange={handleImagesChange}
            className="w-full border border-gray-300 rounded p-2"
          />

          {/* Show Selected Images */}
          <div className="flex flex-wrap gap-4 mt-4">
            {productData.featured_image.map((image, index) => (
              <div key={index} className="relative w-32 h-32">
                {/* Image Preview */}
                <img
                  src={image}
                  alt={`Preview ${index}`}
                  className="w-full h-full object-cover rounded"
                />
                {/* Remove Icon */}
                <button
                  type="button"
                  onClick={() => handleRemoveImage(index)}
                  className="absolute top-0 right-0 bg-red-500 text-white rounded-full w-6 h-6 flex items-center justify-center"
                >
                  &times;
                </button>

///////////////////////////////////////////////////////////////

// Handle multiple image uploads
  const handleImagesChange = (e) => {
    const files = Array.from(e.target.files);
    const images = files.map((file) => {
      const reader = new FileReader();
      return new Promise((resolve) => {
        reader.onloadend = () => resolve(reader.result);
        reader.readAsDataURL(file);
      });
    });

    Promise.all(images).then((base64Images) => {
      setProductData({
        ...productData,
        featured_image: [...productData.featured_image, ...base64Images],
      });
    });
  };




// Remove image by index
  const handleRemoveImage = (index) => {
    const updatedImages = productData.featured_image.filter(
      (_, i) => i !== index
    );
    setProductData({ ...productData, featured_image: updatedImages });
  };
