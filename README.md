# waterFlowLayout

## 怎么使用

###  初始化
	
* 初始化数据（从plist加载）

 		 NSArray *newShops = [Shop objectArrayWithFilename:@"2.plist"];
   		 [self.shops addObjectsFromArray:newShops];
   		
* 初始化瀑布流控件
		
		WaterFlowView *waterFlowView = [[WaterFlowView alloc] init];
	    self.waterFlowView = waterFlowView;
	    waterFlowView.frame = self.view.bounds;
	    waterFlowView.delegate = self;
	    waterFlowView.dataSouce = self;
	    // 跟随父控件的尺寸而自动伸缩
	    waterFlowView.autoresizingMask = UIViewAutoresizingFlexibleWidth | 		UIViewAutoresizingFlexibleHeight;

* 加载数据

		// 加载新的数据
	    [waterFlowView addHeaderWithTarget:self action:@selector(loadNewShops)];
	    // 加载更多数据
	    [waterFlowView addFooterWithTarget:self action:@selector(loadMoreShops)];
	    
	    
### 数据源方法

	- (NSInteger)numberOfCellInWaterFlowView:(WaterFlowView *)waterFlowView {
    return self.shops.count;
    }

	- (NSUInteger)numberOfColumnsInWaterFlowView:(WaterFlowView *)waterFlowView {
	    if (UIInterfaceOrientationIsPortrait(self.interfaceOrientation)) {
	        return  3; //如果是竖屏 返回3列
	    } else {
	        return 5;
	    }
	}
	
	- (WaterFlowViewCell *) waterFlowView:(WaterFlowView *)waterFlowView cellAtIndex:(NSUInteger)index {
	    
	    ShopCell *cell = [[ShopCell alloc] initCellWithWaterFlowView:waterFlowView];
	    
	    cell.shop = self.shops[index];
	    return cell;
	  
	}
	
### 代理方法

	- (CGFloat) waterFlowView:(WaterFlowView *)waterFlowView heightAtIndex:(NSUInteger)index {
	    Shop *shop = self.shops[index];
	    
	    //根据cell的宽度 和 图片的宽高比
	    return waterFlowView.cellWidth * shop.h / shop.w;
	    
	}
	- (CGFloat) waterFlowView:(WaterFlowView *)waterFlowView marginForType:(WaterFlowViewMarginType)marginType {
	    switch (marginType) {
	        case WaterFlowViewMarginTypeTop: return 30;
	        case WaterFlowViewMarginTypeBottom: return 50;
	        case WaterFlowViewMarginTypeLeft: return 10;
	        case WaterFlowViewMarginTypeRight: return 10;
	       
	    
	        default: return 5;
	           
	    }
	}
	- (void)waterFlowView:(WaterFlowView *)waterFlowView didSelectAtIndex:(NSUInteger)index {
	    NSLog(@"点击了第%ld个cell",index);
	}
	
### 框架采用MJExtension进行数据解析，SDWebImage图像缓存，MJRefresh刷新，
	
### 效果图

![](http://7xosrq.com1.z0.glb.clouddn.com/QQ20161114-5.png?e=1479094588&token=BsduBndXasPKM3kxbowJ9Y6Gq-NTYlMJsNrrgMEy:LTukh1lFGAhQQv-z_3rE8rpBwSo)

![](http://7xosrq.com1.z0.glb.clouddn.com/QQ20161114-6.png?e=1479094590&token=BsduBndXasPKM3kxbowJ9Y6Gq-NTYlMJsNrrgMEy:59RCjNlp4-JW1QwCBvTksUwDzhM)